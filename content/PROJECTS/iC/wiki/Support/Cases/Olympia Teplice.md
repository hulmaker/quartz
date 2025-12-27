# Reklamace 2023-12-05 - Decathlon

Clickup task: 86bwn3p4v

## Sensors

dec-001-outdoor

## Problem summary

Manuální měření sedí s cloudem za 04.12.2023 - 11:00, manuální měření nesedí s cloudem (325 vs. Cloud 165) za 04.12.2023 - 16:00

## Komunikace

včera jsme udělali ruční kontrolní měření návštěvnosti na čidlo DECATHLON.

Fyzicky jsme čárkovali zákazníky, kteří prošli vstupem do prodejny DECATHLON.

V časovém úseku 11:00 – 12:00 hod jsme napočítali 91 lidí.

V časovém úseku 16:00 – 17:00 hod jsme napočítali 325 lidí.

Nejsem ji jistá, na jaké číslo mám v reportu koukat, když jde o časový úsek 11:00 – 12:00 – zda je za tento časový úsek číslo na grafu pod 11 hodinami nebo pod 12 hodinami. Pokud je to pod 11 hodinami, pak číslo souhlasí (91).

Nicméně u odpoledního kontrolního počítání číslo nesedí vůbec, ať koukám na 16 nebo 17 hodinu v grafu.

Možná to mám chybně vyexportované, ale pokud chci návštěvnost po hodinách, jinou možnost, než tuto jsem nenašla.

Mohla byste se na to prosím podívat, proč číslo nesouhlasí?

Číslo je dvojnásobné, nemohlo se stát, že jste počítali pro odpolední hodinu oba směry a ne jen vstupy?

## Potenciální problémy

Venkovní senzor, mohl se mlžit

## Summary

Pozn: EG: Decathlon, Actual Period: Mon 04.12.2023 -- Mon 04.12.2023

# 2024-01-05 Velká čísla když měli zavřeno

Venkovní sensor: dec-001-outdoor

- Senzor je venkovní a je tam velmi špatné osvětlení.
- Když měli zavřeno a zhasnuto, začal reportovat desetinásobný nárůst čísel
- Nejspíš je to kvůli tomu, že když vezmeme černý obrázek a normalizujeme, dáme prakticky jen šum do detektoru, tak hlásí nesmysly.
- Předáno na dev, budou se tím zabývat.