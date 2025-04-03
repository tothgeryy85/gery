# valami

def beolvas_fajlbol(fajlnev): """ Beolvassa a fájl tartalmát és visszaadja a sorokat listaként. """ try: file = open(fajlnev, "r", encoding="utf-8")  # Fájl megnyitása olvasásra sorok = file.readlines()  # Sorok beolvasása file.close()  # Fájl bezárása return sorok except FileNotFoundError: print("Hiba: A fájl nem található!")  # Hibaüzenet, ha a fájl nem létezik return []

def konyv_dict(sor): """ Egy sorból létrehoz egy könyv dictionary-t. """ try: adatok = sor.strip().split(";")  # Adatok szétválasztása pontosvessző alapján return {"author": adatok[0], "title": adatok[1], "published_date": int(adatok[2])}  # Dict létrehozása except IndexError: print("Hiba: Hibás adat a fájlban!")  # Hibaüzenet, ha a sor nem megfelelő return {}

def keres_konyvek(lista, keres_tipus, keres_kifejezes): """ Keresés a könyvek listájában a megadott feltétel szerint. """ talalatok = [] for konyv in lista: if keres_tipus in konyv and str(konyv[keres_tipus]).lower() == keres_kifejezes.lower(): talalatok.append(konyv)  # Ha egyezik az érték, hozzáadjuk a találatokhoz return talalatok

def main(): """ A program fő része, amely beolvassa az adatokat, majd lehetőséget ad keresésre. """ fajlnev = "68_konyvek.txt" sorok = beolvas_fajlbol(fajlnev)  # Fájl beolvasása konyvek = [konyv_dict(sor) for sor in sorok if konyv_dict(sor)]  # Könyvek listába mentése

while True:
    print("Mit szeretnél keresni? (szerző/cím/év, vagy kilépés: exit)")
    keres_tipus = input().strip().lower()
    
    if keres_tipus == "exit":  # Kilépés, ha a felhasználó ezt kéri
        print("Kilépés...")
        break
    
    if keres_tipus not in ["author", "title", "published_date"]:
        print("Hiba: Rossz keresési feltétel! Próbáld újra.")  # Hibás keresési kulcs esetén
        continue
    
    print("Add meg a keresett kifejezést:")
    keres_kifejezes = input().strip()
    
    talalatok = keres_konyvek(konyvek, keres_tipus, keres_kifejezes)  # Keresés a könyvek között
    
    if talalatok:
        print("Találatok:")
        for konyv in talalatok:
            print(f"{konyv['author']} - {konyv['title']} ({konyv['published_date']})")  # Találatok kiírása
    else:
        print("Nincs találat!")

if name == "main": main()  # Program indítása

