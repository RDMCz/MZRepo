# SW 04 – Spojové struktury

## Spojové struktury

* Struktura obsahující soubor záznamů (uzlů) propojených pomocí referencí (odkaz/ukazatel)
* Spoj vyjadřuje vztah předchůdce–následník
* Ve zřetězené struktuře musí mít každý prvek odkaz na další prvek (v nezřetězené struktuře probíhá přístup k dalšímu prvku pomocí dopočítávání adresy v paměti)

## Spojové seznamy

* Struktura realizující seznam dynamické délky
* Každý prvek seznamu obsahuje datovou část a odkaz na další prvek v seznamu
* Může být i obousměrný nebo kruhový

``` csharp
// class LinkedList<T>
internal class Node
{
    public T value;
    public Node next;
}

private Node first; // První prvek seznamu (nazýván také 'head' nebo 'start')
```

### Procházení seznamu

``` csharp
public T this[int index] {
    get {
        // Začne u prvního prvku
        Node pointer = first;
        // Přes odkaz .next cyklicky prochází
        for (int i = 0; i < index; i++) {
            // Pokud dostane hodnotu mimo rozsah, vrací poslední prvek (při záporné hodnotě vrací první prvek)
            if (pointer.next != null) {
                pointer = pointer.next;
            }
            else break;
        }
        return pointer.value;
    }
}

```

### Vkládání prvků do seznamu

``` csharp
// Přidá prvek na začátek a změní hlavičku
public void Add(T _value)
{
    Node node = new Node();
    node.value = _value;
    node.next = first;
    first = node;
}
```

* Pro přidání jinam než na začátek se musí změnit _.next_ předchozího na nově přidaný (_.next_ nově přidaného odkazuje prvek, na který dříve odkazoval přechozí)
* Pro přidání na konec se musí celý seznam "projet"

### Odstraňování prvků ze seznamu

``` csharp
// Smaže první prvek
public void DelFirst()
{
    if (first != null) first = first.next;
}
// Smaže vše
public void Clear()
{
    first = null;
}
```

* Pro odstranění libovolného prvku se _.next_ prvku před ním nastaví na prvek za ním

## Spojové stromy

* Uzel má několik následníků (v binárním stromu dva)
* Prvky jsou obvykle nějak seřazené
* [Využití](https://stackoverflow.com/questions/2130416/what-are-the-applications-of-binary-trees)

``` csharp
// class BinaryTreeDictionary<K, V> where K : IComparable where V : IComparable
internal class Node
{
    public K key;
    public V value;
    public Node left;
    public Node right;
}

private Node root; // Výchozí bod stromu je kořen
```

### Procházení stromu

``` csharp
// Najít hodnotu podle klíče (rekurzivní průchod) (klíče seřazeny dle velikosti)
public V this[K key] {
    get {
        return KeyToValue(key, root);
    }
}

public V KeyToValue(K k, Node iroot)
{
    if (iroot == null) throw new Exception("Strom je prázdný");

    if (iroot.key.CompareTo(k) == 0) return iroot.value;
    else if (iroot.key.CompareTo(k) > 0 && iroot.left != null) return KeyToValue(k, iroot.left);
    else if (iroot.key.CompareTo(k) < 0 && iroot.right != null) return KeyToValue(k, iroot.right);

    throw new Exception("Nenalezeno");
}
```

### Vkládání prvků do stromu

``` csharp
// Přidá nový list (list = uzel bez potomků) (klíč musí být unikátní)
public void Add(K k,V v)
{
    var node = new Node() {
        key = k,
        value = v,
        left = null,
        right = null
    };

    if (root == null) { root = node; return; }

    Insert(root, node);
}

private void Insert(Node iroot, Node node)
{
    if (iroot.key.Equals(node.key)) throw new Exception("Klíč již existuje");
    else if (node.key.CompareTo(iroot.key) < 0) { // node.key < iroot.key
        if (iroot.left == null) iroot.left = node;
        else Insert(iroot.left, node);
    }
    else { // node.key > iroot.key
        if (iroot.right == null) iroot.right = node;
        else Insert(iroot.right, node);
    }
}
```

### Odstraňování prvků ze stromu

* Pokud se maže list (prvek bez potomků), stačí na něj smazat odkaz
* Pokud má jednu větev, je vynechán (podobně jako spojový seznam)
* Pokud má oba následníky:
  * Je vynechán: jeho předchůdce, který na něj odkazoval, nyní odkazuje na jeho levého potomka
  * Z tohoto levého potomka se jede doprava, dokud se nenarazí na uzel, který nemá pravého potomka
  * Jako pravý potomek tohoto uzle se nastaví pravý potomek uzle, který je mazán

## Výhody a nevýhody

* __+__ Větší volnost tvorby
* __+__ ~Rychlejší pro manipulaci s daty
* __-__ Pomalejší pro náhodný přístup k datům (musí se k ní "dojít" přes odkazy)
* __-__ Zabírají o trochu více místa v paměti
