# HW 29 – Grafické karty

## Grafická karta

* PC komponenta zajišťující grafický výstup na zobrazovací zařízení (monitor, projektor, ...)

### GPU – Graphics Processing Unit

* Provádí grafické výpočty
* Je přizpůsoben pro rychlou práci s videopamětí, kde vytváří obraz pro vykreslení
* Oproti CPU má o dost více jader a ALU
* Tento čip může být i integrovaný v CPU, kdy je mu poskytnuta část paměti RAM
  * V minulosti se IGPU nacházely i v Northbridge
  * Výhodou IGPU je spotřeba a cena, ~výkonem se ovšem s dedikovanými kartami nemůže rovnat

### Sběrnice

* V minulosti ISA, PCI, AGP
* V současnosti PCIe – Peripheral Component Interconnect Express

### Video paměť

* Kapacita se pohybuje mezi 2 až 24 GB
* Typ paměti je GDDR – DDR SDRAM přizpůsobená pro práci s GPU
* Alternativou je 3D paměť HBM (High Bandwidth Memory) od AMD – nižší spotřeba, širší sběrnice ale drahá výroba

### RAMDAC – RAM Digital-to-Analog Converter

* Převádí digitální data z paměti na analogový signál pro zobrazení na analogovém monitoru (CRT) nebo přenos po analogovém médiu (VGA)

### Výstupní rozhraní

* VGA – Video Graphics Array, "D-sub"
  * Analogové rozhraní, potýkalo se s degradací kvality, ale používá se dodnes
* DVI – Digital Visual Interface
  * DVI-D – digitální / DVI-A – analogový / DVI-I – digital i analog
  * Původní single-link a pozdější dual-link umožňující vyšší rozlišení
* HDMI – High-Definition Multimedia Interface
  * Digitální přenos audia a videa (nebo i Ethernet)
* DP – DisplayPort
  * Myšleno jako koexistence s HDMI a náhrada za staré video rozhraní (VGA, DVI, SCART)
  * Pomocí adaptérů zpětně kompatibilní s VGA a DVI
  * Převážně určen pro video, dokáže ale přenášet i audio, USB, ...
  * DP signál lze přenášet i přes USB-C nebo ThunderBolt

### Parametry

* Grafický čip – Nvidia/AMD/(Intel)
* Kapacita VRAM – 16 GB
* Šířka datové sběrnice – kolik dat proteče za jeden takt mezi GPU a VRAM – 256 bit
* Konektivita – HDMI/DP/...

### Akcelerace

* Obecně – Specifické výpočty se výkonávají na specializovaném hardwaru namísto softwarových výpočtů na univerzálním CPU
* GPGPU – General-Purpose computing on GPUs – využití masivně paralelní GPU pro výpočet obecných algoritmů
  * Vhodné jsou výpočty s daty, které mají podobný formát jako grafická primitiva a mají mezi sebou minimální vazby
  * CUDA vs OpenCL
* Ray-tracing hardware – speciální hardware pro akceleraci výpočtů sledování paprsku

### Vytváření 3D scény

* 3D scéna obsahuje modely, které se skládají z primitiv jako např. polygonů
* Vrcholy těchto primitiv se nazývají vertexy a obsahují souřadnice svého umístění
* Vykreslovací řetězec (graphics pipeline) je sekvence procesů převádějící virtuální 3D scénu na zobrazitelný 2D obraz
* Mezi aplikací a GPU se nachází API mezivrstva, která umožňuje aplikacím univerzálně komunikovat s různými GPU (Direct3D, OpenGL, Vulcan)
* __Input Assembler__ načítá geometrická data primitiv a následně je sestavuje v pomyslném 3D prostoru GPU
* __Teselace__ rozděluje polygony na menší čímž zvyšuje detail objektu, nebo slučuje polygony a detail snižuje
* __Rasterizer__ převádí trojrozměrná primitiva do 2D obrazu. Barvy jejich pixelů vypočítává pixel shader, který dostává data od rasterizeru a vzorkovače textur
* __Output Merger__ provádí test hloubky v Z-bufferu, zobrazí pixely nejblíže kameře a ty "schované" zahodí jako neviditelné

### Negrafické výpočty

* Výkon GPU roste rychleji a už je několikrát větší než CPU
* Výkon měřen v GFLOPS – milion operací s plovoucí řádovou čárkou za sekundu
* CPU je univerzální, optimalizován pro sekvenční zpracování instrukcí (fronta, pipelining, eliminace skoků, ...)
* GPU je vysoce paralelní, jejím hlavním účelem je vykreslování obrazu, v určitých jiných operacích může být nepřesná / nemá vhodné prostředky
* Technologie Nvidia CUDA nebo OpenCL je softwarová vrstva poskytující přímý přístup k instrukční sadě GPU
* Distribuované výpočty – Folding@home, GPUGRID, Seti@home
