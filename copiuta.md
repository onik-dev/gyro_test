**Laboratorul 1 --- Vectori**

-   **1. Conceptul de vector:** Segment de dreaptă orientat, definit
    prin **direcție**, **sens** și **magnitudine** (lungime). Reprezintă
    poziții, viteze sau forțe în joc.

-   **2. Vectori în programare:** Structuri de date (ex. Vector2,
    Vector3) care stochează componentele scalare pe axe: (x, y) sau (x,
    y, z).

-   **3. Produsul scalar (Dot Product):** A\*B = x_A x_B + y_A y_B.
    Rezultatul este un scalar.

    -   \> 0 \--\> unghiul \< 90 grade (obiectul e în față)

    -   = 0 \--\> vectori perpendiculari (90 grade)

    -   \< 0 \--\> unghiul \> 90 grade (obiectul e în spate)

    -   Dacă vectorii sunt normalizați, produsul scalar returnează
        direct cosinusul unghiului dintre ei.

-   **4. Adunarea vectorială:** A + B = (x_A + x_x, y_A + y_y)\$. Se
    adună componentele corespondente. Rezultatul este un vector care
    deplasează originea lui B în vârful lui A.

-   **5. Sisteme de coordonate:**

    -   *Local (Object Space):* Relativ la centrul obiectului.

    -   *Global (World Space):* Relativ la originea întregii scene
        (0,0,0).

-   **6. Normalizarea vectorului:** Transformarea unui vector într-unul
    cu lungimea (magnitudinea) egală cu 1 (vector unitar), păstrând
    direcția.

    -   Formulă: hat-V = V / \|\|V\|\|, unde lungimea \|\|V\|\| =
        radical din x\^2 + y\^2.

-   **7. Definirea unei drepte:** Formă parametrică: P(t) = P_0 + t \*
    D, unde P_0 este un punct inițial, D este vectorul de direcție
    (normalizat), iar t este un scalar (timpul/distanța).

**Laboratorul 2 --- Grile și algoritmi**

-   **1. Interpolarea liniară (Lerp):** Găsirea unei valori intermediare
    între două puncte bazat pe un factor t.

    -   Formulă: Lerp(A, B, t) = A + t \* (B - A), unde t apartine \[0,
        1\].

-   **2. Sistemul de coordonate al grilei:** Spațiu discret (matrice de
    celule). Conversia din coordonate globale în coordonate de grilă:

    -   cellX = floor(worldX / cellSize)

    -   cellY = floor(worldY / cellSize)

-   **3. Vecinii celulelor în grilă:**

    -   *4-vecini (Von Neumann):* Sus, Jos, Stânga, Dreapta \--\>
        offsets: (0,1), (0,-1), (-1,0), (1,0).

    -   *8-vecini (Moore):* Include și diagonalele \--\> adaugă (+- 1,
        +- 1).

-   **4. Raycast bazat pe grilă:** Algoritmul **DDA (Digital
    Differential Analysis)** sau **Amanatides-Woo**. Avansează raza din
    celulă în celulă calculând intersecția cu muchiile grilei pe baza
    pantei razei, evitând verificarea obiectelor pixel cu pixel.

-   **5. Generarea numerelor aleatoare:** Motoarele folosesc PRNG
    (Pseudo-Random Number Generators). Generarea se bazează pe un
    **Seed** (sămânță). Același Seed va genera mereu exact aceeași
    secvență de numere (esențial pentru generarea procedurală
    replicabilă).

-   **6. Diagonalitatea celulelor:** Distanța pe diagonală între
    centrele a două celule este \--\> radical din 2 \* cellSize \~ 1.41
    \* cellSize. În pathfinding (ex. A\*), mișcarea pe diagonală trebuie
    să aibă un cost mai mare (ex. 14 față de 10 pentru ortogonal).

-   **7. Optimizări:** *Spatial Partitioning* -- maparea obiectelor
    dinamice doar în celulele grilei pe care le ocupă, reducând
    complexitatea căutării de la O(N\^2) la O(1) pentru vecini.

**Laboratorul 3 --- Coliziuni**

-   **1. Condițiile coliziunii:** Suprapunerea geometrică a două volume
    de coliziune (Colliders) în același cadru de timp.

-   **2. Fazele detectării coliziunilor:**

    -   **Broad-phase (Faza brută):** Filtrare rapidă a perechilor de
        obiecte care sunt prea departe pentru a se ciocni. Folosește
        volume simple (AABB, sfere) sau partiționare spațială.
        Complexitate redusă.

    -   **Narrow-phase (Faza fină):** Verificare geometrică exactă doar
        pentru perechile rămase din Broad-phase. Determină punctul exact
        de impact, normala coliziunii și adâncimea de penetrare (ex:
        algoritmul SAT -- Separating Axis Theorem).

-   **3. Răspunsul la coliziune:**

    -   *Separarea:* Mutarea obiectelor înapoi de-a lungul *normalei de
        coliziune* cu distanța de penetrare pentru a opri suprapunerea.

    -   *Impulsul:* Modificarea vectorilor de viteză conform legii
        conservării impulsului și a coeficientului de restituire e
        (elasticitate: 0 = plastic, 1 = perfect elastic).

-   **4. Algoritmul Sweep-and-Prune:** Algoritm de Broad-phase.
    Proiectează bounding box-urile (AABB) pe o axă (ex. axa X). Sortează
    punctele min/max ale intervalelor. Dacă intervalele a două obiecte
    pe axa X nu se suprapun, coliziunea este imposibilă și sunt
    eliminate (\"pruned\").

-   **5. Simularea discretă a coliziunilor:** Verificarea coliziunilor
    doar la momente fixe de timp (t, t + \\Delta t).

    -   *Problemă:* **Tunneling** (obiectele foarte rapide trec prin
        obstacole subțiri într-un singur cadru deoarece poziția trece
        direct dinaintea în spatele obstacolului). Rezolvare: CCD
        (Continuous Collision Detection - simulare continuă prin
        raycasting/swept volumes).

-   **6. Optimizări:**

    -   *Bounding Volume Hierarchies (BVH):* Gruparea obiectelor în
        ierarhii de sfere/cutii.

    -   *Collision Layers/Matrix:* Filtrarea coliziunilor din cod (ex.
        gloanțele aliatului nu colizionează cu aliatul).

    -   *Sleeping State:* Dezactivarea calculului fizic pentru obiectele
        rigide care s-au oprit din mișcare și au viteza sub o anumită
        limită.

**Laboratorul 1 --- Vectori**

-   **1. Concept:** Orientat: direcție, sens, magnitudine (lungime).

-   **2. Programare:** Structuri Vector2/Vector3 cu componente (x, y,
    z).

-   **3. Produsul scalar:** \$A \\cdot B = x_A x_B + y_A y_B\$. \$\>0\$
    (față), \$=0\$ (perpendicular), \$\<0\$ (spate). Normalizat =
    \$\\cos(\\theta)\$.

-   **4. Adunare:** \$A + B = (x_A + x_B, y_A + y_B)\$. Deplasare
    combinată.

-   **5. Coordonate:** Local (relativ la obiect) vs. Global (relativ la
    scenă).

-   **6. Normalizare:** \$\\hat{V} = \\frac{V}{\|\|V\|\|}\$ (aduce
    lungimea la \$1\$). \$\|\|V\|\| = \\sqrt{x\^2 + y\^2}\$.

-   **7. Dreaptă:** Parametric: \$P(t) = P_0 + t \\cdot D\$ (\$P_0\$ =
    start, \$D\$ = direcție, \$t\$ = timp/scalar).

**Laboratorul 2 --- Grile și algoritmi**

-   **1. Lerp:** \$A + t \\cdot (B - A)\$, unde \$t \\in \[0, 1\]\$.
    Interpolează între \$A\$ și \$B\$.

-   **2. Grilă:** Spațiu discret. cell = floor(world / cellSize).

-   **3. Vecini:** 4-vecini (ortogonal) vs. 8-vecini (ortogonal +
    diagonal).

-   **4. Raycast grilă:** Algoritm **DDA** / **Amanatides-Woo**.
    Avansează din celulă în celulă după pantă.

-   **5. Random:** PRNG bazat pe **Seed** (sămânță). Același seed =
    aceleași numere.

-   **6. Diagonalitate:** Distanța pe diagonală \$\\approx 1.41 \\cdot
    cellSize\$. Cost mai mare în pathfinding.

-   **7. Optimizare:** *Spatial Partitioning* (obiecte în celule).
    Căutare vecini din \$O(N\^2)\$ în \$O(1)\$.

**Laboratorul 3 --- Coliziuni**

-   **1. Condiție:** Suprapunere geometrică a două volume (colliders).

-   **2. Faze:**

    -   *Broad-phase:* Filtrare brută/rapidă (AABB, sfere). Elimină
        perechile îndepărtate.

    -   *Narrow-phase:* Calcul exact (punct impact, normală, penetrare).
        Ex: algoritmul SAT.

-   **3. Răspuns:** *Separare* (mutare înapoi pe normală) + *Impuls*
    (schimbare viteze prin coeficientul \$e\$).

-   **4. Sweep-and-Prune:** Broad-phase. Proiectează și sortează
    bounding-urile pe o axă pentru a elimina non-suprapunerile.

-   **5. Simulare discretă:** Verificare la cadre fixe (\$t, t+\\Delta
    t\$). Produce **Tunneling** (trecere prin pereți). Soluție: CCD.

-   **6. Optimizări:** **BVH** (ierarhii), **Layers** (matrice de
    filtrare), **Sleeping** (dezactivare fizică la repaus).
