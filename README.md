# rtudip-dip225-project-PavelsPonatovskis
## Projekta autors - Pāvels Poņatovskis

</br>

### Projekta skaidrojums
Mūsdienu pasaulē laba videokarte (GPU) ir nepieciešama dažādu skaitļošanas uzdevumu veikšanai, jo īpaši spēļu pasaules un grafikas intensīvu lietojumprogrammu kontekstā. Ir ļoti svarīgi izdarīt pareizo izvēli, kas atbilst visiem lietotāja kritērijiem. Pirmā problēma ir tā, ka videokaršu tirgus ir dinamisks un cenas bieži var mainīties. Otra problēma ir tā, ka ir daudz dažādu kritēriju - ražotājs, sērija, atmiņas taktiskā frekvence, ieteicamā barošanas bloka (PSU) jauda, gigabaitu daudzums utt. Tas nozīme, ka GPU meklēšanas procesa automatizācija var būt ļoti noderīga un laikietilpīga. 

### Uzdevums 
Izmantojot __Selenium bibliotēku__ automatizēt videokartes meklēšanas procesu iepirkšanās vietā "1a.lv" ar šādiem kritērijiem:
* Sērija: RTX™ 4060
* Cena : Zem 370 Eiro
* Barošanas bloka jauda : 550 W 

Rezultāts ir jāparāda ērtā veidā : Izmantojot __Openpyxl bibliotēku__ ir jāizveido EXCEL tabula, kur ailē 'A' tiek saglabāti videokartes pilnie nosaukumi, bet ailē 'B' - šīs videokartes cenas

### Izmantotas Python bibliotēkas
Šim projektam ir nepieciešamas trīs bibliotēkas - "Selenium" un "Openpyxl" un arī "time"

* __Selenium__ - Lai automatizētu noteiktas darbības tīmekļa lapās, tiek izmantots Selenium. Selenium atbalsta elementu atrašanu, pamatojoties uz dažādām stratēģijām, piemēram, "element class", "element ID", "XPath expressions", "CSS Selectors" utt. Pēc tam ar šādiem elementiem var veikt vairākas darbības, kas ļauj automātiski strādāt ar tīmerkļa lapu. Vairāk informācijas : https://www.selenium.dev/

Projektā Selenium bibliotēka tiek izmantota, lai atvērtu vietni "1a.lv" un veikto pareizo navigāciju, pareizas darbības, lai no mājas lapas iegūtu nepieciešamo informāciju. 

* __Openpyxl__ - Openpyxl ir Python bibliotēka, ko izmanto lasīšanai no Excel faila vai rakstīšanai Excel failā. Vairāk informācijas : https://openpyxl.readthedocs.io/en/stable/

Projektā Openpyxl bibliotēka tiek izmantota, lai izveidotu jaunu EXCEL failu un pēc tam ierakstītu iegūto informāciju noteiktās EXCEL lapas šūnās, kā arī noteiktā veidā formatētu informāciju šūnās. 

* __time__ - Šis modulis nodrošina dažādas ar laiku saistītas funkcijas. Vairāk informācijas: https://docs.python.org/3/library/time.html

Projektā, izmantojot Selenium bibliotēku, ir svarīgi to izveidot tā, lai mijiedarība ar tīmekļa lapas elementiem tiktu veikta tikai pēc šīs tīmekļa lapas pilnīgas ielādes. Tieši tāpēc tiek izmantota time bibliotēka. 

### Programmas darbs:

__1.__ Pirmkārt, tiek pievienotas visas nepieciešamās bibliotēkas. Selenium bibliotēkai tiek pievienotas šādas klases: 
* Service (no moduļa selenium.webdriver.chrome.service) - šī klase ir atbildīga par chrome draivera palaišanu un apturēšanu
* By (no moduļa selenium.webdriver.common.by) - šī klase ir nepieciešama, lai tīmekļa lapā atrastu noteiktus elementus
* Keys (no moduļa elenium.webdriver.common.keys) - šī klase ir atbildīga par taustiņu ieviešanu tastatūrā (tas būs nepieciešams vietnese "1a.lv" struktūras dēļ

Openpyxl tiek pievienotas šādas klases:
* Font (no moduļa openpyxl.styles) - šī klase ir nepieciešama, lai mainītu fontu EXCEL failā 
* Alignment (no moduļa openpyxl.styles) - šī klase ir nepieciešama, lai mainīu teikta līdzinājumu EXCEL failā
* Workbook (no moduļa openpyxl) - šī klase tiek izmantota, lai piekļūtu EXCEL failam un veiktu tajā izmaiņas

__2.__ Otrkārt, programma atver vietni "1a.lv" (pilnekrāna režīmā, izmantojot driver.maximize_window()) un veic navigāciju pa dažādiem vietnes elementiem. Navigācija vietnē notiek šādā secībā: 
* Ekrāna apakšējā daļā tiek nospiesta poga "Akceptēt visu"
* Meklēšanas lodziņā tiek rakstīts teksts "RTX 4060"
* Tiek nospiesta zaļā poga tuvu meklēsanas lodziņai, kas apstiprina meklēšanu 
* Tiek spiesta kategorija "Video kartes"
* Mājas lapa tiek pārvietota uz leju par 500 pikseļiem un cenas limits tiek noteikts 370 eiro

__3.__ Pēc tam tiek pārbaudīts, kuras videokartes var iekļaut rezultātā un kuras nevar. Mājas lapas "1a.lv" struktūras dēļ rezultātā tiek parādīti vairāki modeļi. Tas nozīmē, ka, izmantojot "IF statement", ir jāpārbauda informāciju : ja modeļa nosaukums ir "RTX™ 4060" un ja barošanas bloka jauda ir 550 W, šīs grafiskās kartes nosaukumi un cena tiek pievienoti attiecīgajā sarakstā. 

__4.__ Beigās tiek izveidots EXCELL fails "result.xlsx", vērtības no sarakstiem "GPU_titles_list" un "GPU_prices_list" tiek ierakstītas attiecīgi A un B kolonnā. Lai iegūtu labāku stilistosku izskatu, katrai kolonnai tiek izveidoti divi nosaukumi, tiem tiek pievienots "BOLD" stils un tie tiek centrēti, izmantojot "Font" un "Alignment" klases. Timekļa lapa tiek automātiski aizvērta, izmantojot driver.quit()

### Iespējamās problēmas:

* Lai noklikšķinātu uz noteiktiem tīmekļa lapas elementiem, šī tīmekļa lapa ir pilnībā jāielādē. Tieši tāpēc __time.sleep(2)__ tiek rakstīts pēc katras lapas ielādes. Bet, ja programma nedarbojas, varbūt tas ir tāpēc, ka ir nepieciešams vairāk laika, lai ielādētu lapu (jo interneta ātrums un datoru ātrums atšķiras), varbūt jāpalielina vērtība iekšā time.sleep (piemēram 5)

* Vēl viena iespējamā problēma varētu būt rindā: __driver.execute_script("window.scrollTo(0,500)")__. Lapa tiek pārvietota uz leju par 500 pikseļiem, taču, ja ekrāna izšķirtspējs ir lielāka par Full HD (1920x1080), var nepietikt ar 500 pikseļiem un šī vērtība ir jāpalielina. Ja ar 500 pikseļiem nepietiek, elements netiks atrasts un radīsies kļūda. 
