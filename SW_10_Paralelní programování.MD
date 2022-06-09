# SW 10 – Paralelní programování

## Asynchronní programování

* Asynchronní volání neblokují chod volajícího
* Cílem je responzivita aplikace
* Např. aby nezamrzlo UI při stahování dat z databáze
* `async`, `await`

## Paralelní programování

* Rozdělení práce do několika vláken
* Cílem je výkon (rychlost) aplikace
* Např. Quicksort

## Thread

* Třída `Thread` reprezentuje vlákno (tok)
* Aplikace může běžet ve více paralelních vláknech
* `Thread` `.Start()`, `.Sleep()`, `.Join()`, ...

### Vytvoření vlákna

``` csharp
static void MethodA() { }

static void MethodB(object obj) { }

public static void Main(string[] args)
{
    // Pro použití ThreadStart musí metoda vracet void a být bez parametrů
    Thread ta = new Thread(new ThreadStart(MethodA));
    ta.Start();
    // Pro použití ParametrizedThreadStart musí metoda vracet void a mít jeden parametr typu object
    // ten se pak nastavuje ve .Start()
    Thread tb = new Thread(new ParametrizedThreadStart(MethodB));
    tb.Start("foo");
}
```

* Bez specifikování delegáta se kompilátor rozhodne na základně signatury metody:

``` csharp
public static void Main(string[] args)
{
    Thread ta = new Thread(MethodA); // Implicitně přetypováno na ThreadStart
    ta.Start();
    Thread tb = new Thread(MethodB); // Implicitně přetypováno na ParametrizedThreadStart
    tb.Start("foo");
}
```

## Task

* Třída představující asynchronní operaci
* Vyšší úroveň abstrakce než `Thread`, vnitřně implementuje třídu `ThreadPool`
* `Task task = new Task(() => { });` vytvoří úlohu
* `task.Start();` spustí úlohu
* `Task.Run(() => { });` vytvoří a spustí úlohu
* `Task.Factory.StartNew(() => { });` je podobné jako `Task.Run(() => { });`, pouze drobné [rozdíly](https://stackoverflow.com/questions/38423472/what-is-the-difference-between-task-run-and-task-factory-startnew)
* `Task.WaitAll(task);` čeká na dokončení úloh(y), blokuje aktuální vlákno
* `Parallel.Invoke(() => {úloha1}, () => {úloha2}, ...);` vytvoří a spustí úlohy paralelně a počká na jejich dokončení
* `Task.WhenAll(task);` reprezentuje úlohu, která se dokončí, až když skončí všechny úlohy na vstupním parametru

## Parallel.For

* Paralelní průchody cyklem
* `Parallel.For(odInkluzivni, doExkluzivni, (iteracniPromenna) => { });`
* `Parallel.ForEach(kolekce, (iteracniPromenna) => { });`

## Synchronizace vláken

* Synchronizace vláken – koordinovaný přístup ke sdíleným prostředkům
* Při zpracování dat vláknem by k těmto datům neměla mít ostatní vlákna přístup
  * Problém nastává, když vlákno s daty provádí neatomickou operaci a jiné vlákno začne s těmito daty také pracovat
  * (data ještě nejsou plně zpracovaná a připravená k další akci)

### Zámek

``` csharp
static void Main(string[] args)
{
    for (int i = 0; i < 3; i++) new Thread(Method).Start();
}

static object baton = new object();

static void Method()
{
    var id = Environment.CurrentManagedThreadId;
    WriteLine(id + " se snaží dostat do chráněné sekce");
    lock(baton) {
        WriteLine(id + " se nachází ve chráněné sekci");
        Thread.Sleep(10);
        WriteLine(id + " opouští chráněnou sekci");
    }
    Thread.Sleep(10);
    WriteLine(id + " je na konci metody");
}

/* Výstup může vypadat:

4 se snaží dostat do chráněné sekce
5 se snaží dostat do chráněné sekce
6 se snaží dostat do chráněné sekce
4 se nachází ve chráněné sekci
4 opouští chráněnou sekci
5 se nachází ve chráněné sekci
4 je na konci metody
5 opouští chráněnou sekci
6 se nachází ve chráněné sekci
5 je na konci metody
6 opouští chráněnou sekci
6 je na konci metody

*/
```

* `lock()` je syntaktický cukr, lze rozepsat jako:

``` csharp
Monitor.Enter(baton);
try {
    // Chráněná sekce
}
finally {
    Monitor.Exit(baton);
}
```

* `lock()` uzamyká kus kódu objektem, který dostane jako vstupní parametr
  * V tomto kusu kódu může být pouze jedno vlákno, ostatní čekají
  * Vstupním parametrem je kód uzamčen ale samotný parametr nijak uzamčen/chráněn/modifikován není, může to být libovolný object

## async, await

* Klíčová slova usnadňující vytváření asynchronního kódu

``` csharp
private void RunDownload()
{
    string results = DownloadData();
}
```

1. Pokud chceme volat `DownloadData` asynchronně a neexistuje připravená metoda `DownloadDataAsync`, můžeme metodu zabalit do "asynchronní bubliny" `Task.Run`
2. Asynchronní `DownloadData` ale místo `string` vrací `Task<string>`, proto je potřeba použít klíčové slovo `await`
    * __`await` – proveď asynchronně, ale počkej na výsledek__
3. Metoda používající klíčové slovo `await` musí být provedena asynchronně, před návratový typ se tedy připíše klíčové slovo `async`
    * __`async` – modifikátor, který specifikuje, že daná metoda (nebo lambda výraz) je prováděna asynchronně__
4. Asynchronní metoda místo `void` vrací samotný `Task`, u ostatních návratových typů se vrací `Task<navratovyTyp>`
    * Výjimkou jsou události, zde se návratový typ nemění
5. Zvykem je, že na konec názvu asynchronní metody se připíše "Async" (`RunDownload()` → `RunDownloadAsync()`)

``` csharp
private async Task RunDownloadAsync()
{
    string results = await Task.Run(() => DownloadData());
}
```

## Použití paralelismu

* Dva hlavní důvody – výkon (urychlení nějakého výpočtu) a responzivita (jeden výpočet nepozastaví celou aplikaci)

## Ukázka kódu

* Sečíst všechna čísla v poli `int[] numbers`:

### Sekvenčně

``` csharp
static void Main(string[] args)
{
    long sum = 0;

    for (int i = 0; i < numbers.Length; i++) sum += numbers[i];

    WriteLine(sum);
}
```

### Pomocí Thread

``` csharp
static void Main(string[] args)
{
    CPUs = Environment.ProcessorCount; // Vrací počet logických procesorů, které mohou být využity CLR
    portionSize = numbers.Length / CPUs; // Rozdělení pole pro jednotlivá vlákna
    sumPortions = new long[CPUs]; // Pole pro (mezi)výsledky
    long sum = 0;

    // Vytvoření pole vláken a jejich spuštění
    Thread[] threads = new Thread[CPUs];
    for (int i = 0; i < CPUs; i++) {
        threads[i] = new Thread(SumPortion);
        threads[i].Start(i);
    }
    // Počkat, až všechna vlákna skončí
    // .Join() blokuje volající vlákno, dokud dané vlákno neskončí
    for (int i = 0; i < CPUs; i++) threads[i].Join();
    // Sečíst (mezi)výsledky jednotlivých vláken
    for (int i = 0; i < CPUs; i++) sum += sumPortions[i];

    WriteLine(sum);
}

static int CPUs;
static int portionSize;
static long[] sumPortions;

static void SumPortion(object _portionNumber)
{
    int portionNumber = (int)_portionNumber; // Explicitní přetypování
    var start = portionSize * portionNumber;
    var end = (portionNumber == CPUs - 1) ? (numbers.Length) : (portionSize * portionNumber + portionSize);
    // $"Vlákno {Environment.CurrentManagedThreadId}" pracuje od {start} do {end - 1}
    long sum = 0;
    for (int i = start; i < end; i++) sum += numbers[i];
    sumPortions[portionNumber] = sum;
}
```

### Pomocí Task

``` csharp
static void Main(string[] args)
{
    int CPUs = Environment.ProcessorCount;
    int portionSize = numbers.Length / CPUs;
    long[] sumPortions = new long[CPUs];
    long sum = 0;

    Task[] tasks = new Task[CPUs];
    for (int i = 0; i < CPUs; i++) {
        var tid = i; // Pro jistotu
        tasks[tid] = Task.Run(() => {

            var start = portionSize * tid;
            var end = (tid == CPUs - 1) ? (numbers.Length) : (portionSize * tid + portionSize);

            long sum = 0;
            for (int j = start; j < end; j++) sum += numbers[j];
            sumPortions[tid] = sum;

        });
    }

    Task.WaitAll(tasks); // Počká, až se dokončí všechny Tasky v poli

    for (int i = 0; i < CPUs; i++) sum += sumPortions[i]; // Sečíst (mezi)výsledky

    WriteLine(sum);
}
```

### Pomocí Parallel.For

``` csharp
static void Main(string[] args)
{
    int CPUs = Environment.ProcessorCount;
    int portionSize = numbers.Length / CPUs;
    long[] sumPortions = new long[CPUs];
    long sum = 0;

    Parallel.For(0, CPUs, (i) => {

        var tid = i;
        var start = portionSize * tid;
        var end = (tid == CPUs - 1) ? (numbers.Length) : (portionSize * tid + portionSize);

        long sum = 0;
        for (int j = start; j < end; j++) sum += numbers[j];
        sumPortions[tid] = sum;

    });

    for (int i = 0; i < CPUs; i++) sum += sumPortions[i];

    WriteLine(sum);
}
```
