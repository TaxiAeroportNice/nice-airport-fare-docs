# Nice Airport Transfer Fare System: Technical Documentation

**Scope.** This documentation describes how the fare structure, booking inputs and operating rules of a private transfer service at Nice Côte d'Azur airport (NCE) fit together. The source is the public website [https://taxiaeroportnice.com](https://taxiaeroportnice.com/), in particular its [fare table](https://taxiaeroportnice.com/tarifs/), the [help and FAQ page](https://taxiaeroportnice.com/aide-faq/) and the booking form on the homepage. All figures were read on 20 November 2026 (Europe/Paris). Nothing here replaces the live pages, which remain the reference if a price or rule changes.

**Status of the service.** The operator works as a VTC (chauffeur-driven hire vehicle), booked in advance. It is not an official taxi and does not pick up from the taxi rank.

## 1. Fare model

### 1.1 Unit of sale

The unit of sale is a **one-way trip between the airport and a named destination**. The fare page states that every amount applies per trip, and that a return booking is charged once for each leg. A return trip is therefore modelled as two independent records, not as a discounted pair.

### 1.2 What a fare includes

According to the fare page, each published amount already contains:

| Component | Treatment |
|---|---|
| Personal greeting at arrivals | Included |
| Standard luggage | Included |
| Motorway tolls | Included |
| Italian routes: A10 Autostrada dei Fiori tolls, tunnel and ZTL charges where they apply | Included |
| Skis, snowboards, surfboards, golf bags | Carried free of charge |
| Child seat or booster | Free on request |
| Traffic delay or late landing | No supplement; the amount confirmed at booking is final |

### 1.3 Vehicle classes

The table publishes two columns per route, a saloon ("Berline") price and a van price. This documentation uses only the **lowest Standard saloon price** for each route, written as "from X €", because it is the entry point of the scale. Vans are offered for groups of up to eight passengers and for bulky equipment.

## 2. Distance bands

The fare table lists around 80 named destinations, each with a distance, an estimated driving time and a starting price. Grouping them by distance shows how the fixed part of a transfer (greeting, waiting at arrivals, positioning of the car) weighs heavily on short trips and fades on long ones.

| Distance band | Routes in table | Starting fares in band | Example routes |
|---|---|---|---|
| Up to 15 km | 7 | from 34 € to from 61 € | [Saint-Laurent-du-Var](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-saint-laurent-du-var/) 5 km, from 34 €; [Nice centre](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-nice/) 7 km, from 42 € |
| 16 to 30 km | 19 | from 62 € to from 86 € | [Antibes](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-antibes/) 24 km, from 78 €; [Cannes](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-cannes/) 29 km, from 86 € |
| 31 to 50 km | 11 | from 93 € to from 118 € | [Monaco](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-monaco/) 33 km, from 95 €; [Menton](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-menton/) 41 km, from 112 € |
| 51 to 100 km | 26 | from 130 € to from 215 € | [Sanremo](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-sanremo/) 67 km, from 160 €; [Isola 2000](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-isola-2000/) 89 km, from 201 € |
| 101 to 200 km | 14 | from 230 € to from 328 € | [Saint-Tropez](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-saint-tropez/) 107 km, from 236 €; [Savona](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-savone/) 158 km, from 327 € |
| Over 200 km | 3 | from 413 € to from 630 € | [Genoa](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-genes/) 206 km, from 413 €; [Milan](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-milan/) 329 km, from 630 € |

Counts exclude duplicate rows (Sanremo and Portofino appear in two tables). Divided by distance, the starting fare falls from more than 4 € per kilometre on the shortest runs to under 2 € per kilometre beyond 200 km.

### 2.1 Mountain routes and seasonal routing

Ski resorts form a separate table. Vehicles are described as equipped under the Loi Montagne (winter tyres or chains), with ski racks included. Two destinations need a note: for **Barcelonnette** (from 322 €) and **Pra Loup** (from 328 €), the winter price is higher than the table figure. The reason is the route, not the season as such: when the usual mountain road is closed, the car has to take a longer way round. The [ski resorts overview](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-stations-de-ski/) and the [Pra Loup route page](https://taxiaeroportnice.com/taxi-aeroport-nice-vers-pra-loup/) give the details.

## 3. Flight tracking and waiting time

The operating rules around arrival are deterministic and easy to model:

| Rule | Value |
|---|---|
| Flight status | Followed in real time; pickup time adjusted to the actual landing at no extra cost |
| Meeting point | Terminal 1 or Terminal 2, passenger exit after baggage claim, name board |
| Free waiting at the airport | 60 minutes |
| Free waiting at any other pickup place (hotel, home, port, station) | 20 minutes |
| Driver details | Name and phone number sent by SMS or WhatsApp before arrival |
| Service hours | 24 hours a day, 7 days a week, including public holidays |

The 60 minute allowance is generous enough to absorb most passport queues and slow baggage belts, which is why the return direction, with only 20 minutes, needs more care from the passenger.

## 4. Coverage

The fare page groups destinations into regional tables: Nice and its surroundings, Antibes, Cannes, the Pays de Grasse, the Estérel, the Gulf of Saint-Tropez, the Var hinterland, Monaco and Menton, the southern Alps and Italy. It also states that more than 250 destinations in France and Italy are served on request. The [areas served page](https://taxiaeroportnice.com/zones-desservies/) is the entry point for places that do not appear in a table.

The next page, [Booking workflow and data fields](booking-workflow.md), documents what a reservation contains and how changes are handled.

## About the source

This documentation is based on information published by Transfert Privé Aéroport Nice, a private chauffeur service (VTC) for trips to and from Nice Côte d'Azur airport, operated by Stamati Constantin / BLACKCARS. The operator is listed in the EVTC register under number 006250163, with SIRET 537 609 786 00034 and professional liability insurance n°AU457656. Fares are fixed and given before booking, flights are tracked, passengers are greeted with a name board, and the service runs 24 hours a day, 7 days a week. Payment is accepted by Visa, Mastercard or cash, and drivers speak French, English, Italian and Spanish. Contact: Transfert Privé Aéroport Nice, 35 B Rue de France, 06000 Nice, France, +33 7 53 54 87 71, [WhatsApp](https://wa.me/33753548771), [contact@taxiaeroportnice.com](mailto:contact@taxiaeroportnice.com). Online booking: [https://taxiaeroportnice.com](https://taxiaeroportnice.com/).
