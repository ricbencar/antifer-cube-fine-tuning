# Concrete Antifer Cubes

## Executive Summary

Antifer cubes are massive grooved unreinforced concrete artificial armour units used in rubble-mound breakwaters and related maritime protection works. They were developed in the context of the Port of Antifer, in Normandy, during the early 1970s, and entered prototype use in the second half of that decade. The unit belongs to the family of robust massive concrete armour units: it preserves a compact cube-like resistant body, while using four lateral grooves and controlled tapering to improve hydraulic behaviour, interlock and placement stability relative to a simple cube.

The principal engineering conclusion is that Antifer performance cannot be reduced to geometry alone. Hydraulic stability depends strongly on placement method, packing density, armour slope, allowable damage criterion, storm duration and incident wave climate. The dimensional parametrisation is nevertheless important for technical drawings, CAD documentation, volume control and reproducible interpretation of the original Antifer geometry.

The accompanying Python production script generates one closed vectorial Antifer armour-unit solid from input unit weight $W$ and concrete unit weight $W_c$, with selectable **Pita (1986)** and **Carvalho (2026)** dimensional conventions. The same validated boundary-representation is exported as **IFC**, **STL**, **OBJ** and **DXF**, with a plain-text calculation report. The script is a geometric CAD/BIM production and documentation tool; hydraulic stability design remains a separate project-specific verification task.

The production script implements two selectable dimensional conventions using the same vectorial B-rep topology: **Pita (1986)** and **Carvalho (2026)**. The main coefficients are consolidated below so that the reference geometry can be read without searching through dispersed formulae in the document.

| Coefficient | Meaning | Pita (1986) | Carvalho (2026) |
|---|---|---:|---:|
| $K_V=V/H^3$ | non-dimensional volume coefficient | $1.024700000000$ | $1.000000000000$ |
| $f$ | horizontal coefficient factor applied to Pita | $1.000000000000$ | $0.987874174182$ |
| $a=A/H$ | bottom bounding width coefficient | $1.086000000000$ | $1.072831353161$ |
| $b=B/H$ | top bounding width coefficient at $z=H$ | $1.005000000000$ | $0.992813545052$ |
| $d=D/H$ | lateral corner-chamfer coefficient | $0.024000000000$ | $0.023708980180$ |
| $r=R/H$ | circular-groove radius coefficient | $0.121500000000$ | $0.120026712163$ |
| $e=E/H$ | outside groove-centre offset coefficient | $0.025906459610$ | $0.025592322393$ |
| $c_{\rm arc}=C_{\rm arc}/H=r-e$ | generated maximum circular-arc groove inset | $0.095593540390$ | $0.094434389770$ |
| $q=Q/H=\sqrt{r^2-e^2}$ | groove half-opening coefficient | $0.118705961731$ | $0.117266553915$ |
| $2q=2Q/H$ | full groove-opening coefficient | $0.237411923462$ | $0.234533107831$ |

The Carvalho convention is obtained by applying the horizontal normalisation factor $f=0.987874174182$ to the Pita plan and groove coefficients $A/H$, $B/H$, $D/H$, $R/H$ and $E/H$, while keeping $H$ as the vertical reference height. This gives $V/H^3=1.000000$ in the same algebraic volume balance used by Pita.

| Convention | Principal reference | Generated relation | Practical interpretation |
|---|---|---:|---|
| Pita (1986) | historical dimensional ratios | $V/H^3=1.024700$ | Pita proportional geometry with the historical dimensional reference height. |
| Carvalho (2026) | horizontally normalised coefficients | $V/H^3=1.000000$ | CAD/BIM coefficient convention where the reference height equals the volume-equivalent nominal dimension $D_n=V^{1/3}$. |

There is **no top bevel** in the production geometry. The top face is a single horizontal plane at $z=H$, and $B$ is measured directly on that top face. The four corner chamfers are lateral plan chamfers. Each side groove is reconstructed as one continuous circular arc of absolute radius $R$, with no auxiliary straight inner segment.

The complete algebraic volume calculation is tabulated in the geometry section. In compact form, the governing balance is $V/H^3=(a^2+ab+b^2)/3-2d^2-4A_g$, where $A_g$ is the non-dimensional area of one circular groove segment.

## History, Genesis and International Diffusion

The Antifer cube was developed for the Port of Antifer, in Normandy, France, in the early 1970s, with prototype use following in the second half of that decade. The engineering problem was typical of exposed deep-water port works: very large natural armourstone was difficult to secure, while a simple concrete cube did not provide the required hydraulic response. The adopted solution was a compact tapered cube with four lateral grooves.

After the structural-integrity problems experienced by slender concrete armour units in the late 1970s and early 1980s, the Antifer gained prominence as a massive and mechanically robust alternative. Sines, in Portugal, is the clearest example: after the Dolos armour-layer failure, Antifer-type grooved cubes were used in emergency and rehabilitation works, including high-density concrete units in the definitive west-breakwater intervention.

Other representative Antifer applications include Zeebrugge in Belgium, Mohammedia in Morocco, the Douro Bar / Cabedelo do Douro, Leixões, Ponta Delgada and Lajes das Flores in Portugal, and documented manufacture and placement practice in Brunei. These examples show the main fields of use of the unit: prototype development, severe-exposure repair, modern port extensions, island-port reconstruction, overtopping studies and practical production methodology.

## Geometry, Parametrisation and Algebraic Volume Definition

The Antifer unit is modelled as a grooved tapered cube generated directly from algebraic coefficients. The production script uses two homologous horizontal construction sections: the bottom section at $z=0$ with width $A$, and the flat top section at $z=H$ with width $B$. The lateral grooves and corner chamfers are generated in plan and carried through the tapered body by the vectorial B-rep construction.

### Production Geometry Convention

| Item | Adopted convention |
|---|---|
| Vertical reference | $H$ is the total unit height. |
| Bottom section | $A$ is the bottom bounding width at $z=0$. |
| Top section | $B$ is the top bounding width at $z=H$. |
| Top face | Single horizontal top plane; no top bevel. |
| Intermediate level | No separate $H-D$ section is used. |
| Chamfers | $D$ is a lateral plan-chamfer offset. |
| Grooves | Four identical circular side grooves. |
| Groove radius | $R$ is the absolute circular-arc radius; $r=R/H$. |
| Groove centre | $E$ is the outside centre offset; $e=E/H$. |
| Groove depth | $C_{\rm arc}=R-E$; $c_{\rm arc}=r-e$. |
| Groove opening | $Q=\sqrt{R^2-E^2}$; $q=Q/H=\sqrt{r^2-e^2}$. |
| Geometry source | No imported template geometry; the B-rep is generated from the tabulated coefficients. |

### General Non-Dimensional Volume Formulae

| Component | Non-dimensional expression | Meaning |
|---|---:|---|
| Gross tapered square frustum | $K_{\rm frustum}=(a^2+ab+b^2)/3$ | volume before chamfer and groove removals |
| Four plan corner chamfers | $K_{\rm chamfers}=2d^2$ | four triangular plan removals through the unit height |
| One circular groove area | $A_g=r^2\arccos(e/r)-e\sqrt{r^2-e^2}$ | area removed by one side groove in $H^2$ units |
| Four side grooves | $K_{\rm grooves}=4A_g$ | total groove-volume coefficient |
| Final volume coefficient | $K_V=K_{\rm frustum}-K_{\rm chamfers}-K_{\rm grooves}$ | final value of $V/H^3$ |
| Unit volume from inputs | $V=W/W_c$ | concrete volume from unit weight and concrete unit weight |
| Reference height | $H=(V/K_V)^{1/3}$ | dimensional height used by the selected convention |

### Coefficient Set Used by the Production Script

| Quantity | Meaning | Pita (1986) | Carvalho (2026) |
|---|---|---:|---:|
| $K_V$ | final volume coefficient | $1.024700000000$ | $1.000000000000$ |
| $f$ | common horizontal factor | $1.000000000000$ | $0.987874174182$ |
| $a=A/H$ | bottom width coefficient | $1.086000000000$ | $1.072831353161$ |
| $b=B/H$ | top width coefficient | $1.005000000000$ | $0.992813545052$ |
| $d=D/H$ | corner-chamfer coefficient | $0.024000000000$ | $0.023708980180$ |
| $r=R/H$ | groove-radius coefficient | $0.121500000000$ | $0.120026712163$ |
| $e=E/H$ | groove-centre offset coefficient | $0.025906459610$ | $0.025592322393$ |
| $c_{\rm arc}=r-e$ | generated groove-depth coefficient | $0.095593540390$ | $0.094434389770$ |
| $q=\sqrt{r^2-e^2}$ | groove half-opening coefficient | $0.118705961731$ | $0.117266553915$ |
| $2q$ | full groove-opening coefficient | $0.237411923462$ | $0.234533107831$ |

The historical drawing notation commonly reports $C/H=0.095600$ for Pita. The script uses the volume-consistent circular-arc value $c_{\rm arc}=0.095593540390$, which is the generated inset from the solved relation $C_{\rm arc}=R-E$.

### Pita (1986) Full Geometric Volume Calculation

| Step | Calculation | Value |
|-----:|:----------------------------------------------------------------------------------------------|----------------------:|
| 1 | Bottom width coefficient: $a=A/H$ | $1.086000000000$ |
| 2 | Top width coefficient: $b=B/H$ | $1.005000000000$ |
| 3 | Corner-chamfer coefficient: $d=D/H$ | $0.024000000000$ |
| 4 | Groove-radius coefficient: $r=R/H$ | $0.121500000000$ |
| 5 | Groove-centre offset: $e=E/H$ | $0.025906459610$ |
| 6 | Bottom squared term: $a^2$ | $1.179396000000$ |
| 7 | Mixed frustum term: $ab$ | $1.091430000000$ |
| 8 | Top squared term: $b^2$ | $1.010025000000$ |
| 9 | Gross square frustum: $K_{\rm frustum}=(a^2+ab+b^2)/3$ | $1.093617000000$ |
| 10 | Chamfer squared term: $d^2$ | $0.000576000000$ |
| 11 | Four corner chamfers: $K_{\rm chamfers}=2d^2$ | $0.001152000000$ |
| 12 | Net before grooves: $K_{\rm net}=K_{\rm frustum}-K_{\rm chamfers}$ | $1.092465000000$ |
| 13 | One-groove area from balance: $A_g=(K_{\rm net}-K_V)/4$ | $0.016941250000$ |
| 14 | One-groove circular-arc area: $A_g=r^2\arccos(e/r)-e\,q$ | $0.016941250000$ |
| 15 | Generated groove depth: $c_{\rm arc}=r-e$ | $0.095593540390$ |
| 16 | Groove half-opening: $q=\sqrt{r^2-e^2}$ | $0.118705961731$ |
| 17 | Full groove opening: $2q$ | $0.237411923462$ |
| 18 | Four side grooves: $K_{\rm grooves}=4A_g$ | $0.067765000000$ |
| 19 | Final volume coefficient: $K_V=K_{\rm net}-K_{\rm grooves}$ | $1.024700000000$ |
| 20 | Dimensional volume relation: $V=1.024700000000H^3$ | $-$ |
| 21 | Reference height: $H=(V/1.024700000000)^{1/3}$ | $-$ |
| 22 | Height from weight input: $H=(W/(W_cK_V))^{1/3}$ | $-$ |

### Carvalho (2026) Full Geometric Volume Calculation

Carvalho uses the same geometric balance as Pita, with the Pita plan and groove coefficients multiplied by $f=0.987874174182$. Since all horizontal removals are area terms, the volume coefficient scales by $f^2$, giving $1.024700000000\,f^2=1.000000000000$.

| Step | Calculation | Value |
|-----:|:----------------------------------------------------------------------------------------------|----------------------:|
| 1 | Horizontal normalisation factor: $f=(1.000000000000/1.024700000000)^{1/2}$ | $0.987874174182$ |
| 2 | Bottom width coefficient: $a=f\,1.086000000000$ | $1.072831353161$ |
| 3 | Top width coefficient: $b=f\,1.005000000000$ | $0.992813545052$ |
| 4 | Corner-chamfer coefficient: $d=f\,0.024000000000$ | $0.023708980180$ |
| 5 | Groove-radius coefficient: $r=f\,0.121500000000$ | $0.120026712163$ |
| 6 | Groove-centre offset: $e=f\,0.025906459610$ | $0.025592322393$ |
| 7 | Bottom squared term: $a^2$ | $1.150965328389$ |
| 8 | Mixed frustum term: $ab$ | $1.064981966856$ |
| 9 | Top squared term: $b^2$ | $0.985820051296$ |
| 10 | Gross square frustum: $K_{\rm frustum}=(a^2+ab+b^2)/3$ | $1.067255782180$ |
| 11 | Chamfer squared term: $d^2$ | $0.000562115741$ |
| 12 | Four corner chamfers: $K_{\rm chamfers}=2d^2$ | $0.001124231482$ |
| 13 | Net before grooves: $K_{\rm net}=K_{\rm frustum}-K_{\rm chamfers}$ | $1.066131550698$ |
| 14 | One-groove circular-arc area: $A_g=r^2\arccos(e/r)-e\,q$ | $0.016532887674$ |
| 15 | Generated groove depth: $c_{\rm arc}=r-e$ | $0.094434389770$ |
| 16 | Groove half-opening: $q=\sqrt{r^2-e^2}$ | $0.117266553915$ |
| 17 | Full groove opening: $2q$ | $0.234533107831$ |
| 18 | Four side grooves: $K_{\rm grooves}=4A_g$ | $0.066131550698$ |
| 19 | Final volume coefficient: $K_V=K_{\rm net}-K_{\rm grooves}$ | $1.000000000000$ |
| 20 | Dimensional volume relation: $V=H^3$ | $-$ |
| 21 | Reference height: $H=V^{1/3}$ | $-$ |
| 22 | Height from weight input: $H=(W/W_c)^{1/3}$ | $-$ |

### Absolute Dimensions from the Selected Convention

| Dimension | Pita expression | Carvalho expression |
|---|---:|---:|
| $A$ | $1.086000000000H$ | $1.072831353161H$ |
| $B$ | $1.005000000000H$ | $0.992813545052H$ |
| $D$ | $0.024000000000H$ | $0.023708980180H$ |
| $R$ | $0.121500000000H$ | $0.120026712163H$ |
| $E$ | $0.025906459610H$ | $0.025592322393H$ |
| $C_{\rm arc}=R-E$ | $0.095593540390H$ | $0.094434389770H$ |
| $Q$ | $0.118705961731H$ | $0.117266553915H$ |
| $2Q$ | $0.237411923462H$ | $0.234533107831H$ |

### Horizontal Section Definition

| Element | Non-dimensional definition | Geometric role |
|---|---|---|
| Half-width | $h=w/(2H)$ | local half-width of a section with absolute width $wH$ |
| Chamfer example | $(h-d,-h)$ to $(h,-h+d)$ | one corner-chamfer edge in plan |
| East-side inward groove coordinate | $x_{\rm in}(y)=-e+\sqrt{r^2-y^2}$ | local groove indentation, inward positive |
| Groove domain | $-q\le y\le q$ | circular-arc mouth limits |
| East-side global coordinate | $x(y)=h+e-\sqrt{r^2-y^2}$ | actual side coordinate after indentation |
| Groove mouth | $y=\pm q$, $x=h$ | side face remains continuous at the groove ends |
| Deepest groove point | $y=0$, $x=h+e-r=h-c_{\rm arc}$ | maximum side indentation |
| Other sides | 90° rotations | north, west and south grooves are rotational copies |

### Lateral Batter

| Quantity | Pita (1986) | Carvalho (2026) |
|---|---:|---:|
| $(a-b)/2$ | $0.040500000000$ | $0.040008904054$ |
| Main lateral inclination from vertical | $2.3192115955^\circ$ | $2.2911194181^\circ$ |
| Angle between bottom plane and main lateral face | $87.6807884045^\circ$ | $87.7088805819^\circ$ |

### Implemented Production Outputs

The production script writes the following deliverables to the selected output folder:

| Output | Purpose |
|---|---|
| `antifer_<geometry>_<W>kN_Wc<Wc>kNm3.ifc` | IFC4 `IfcFacetedBrep` with the exact production B-rep loops, dimensional properties and quantity data. |
| `antifer_<geometry>_<W>kN_Wc<Wc>kNm3.stl` | Closed triangular surface mesh in metres, generated from the validated export mesh. |
| `antifer_<geometry>_<W>kN_Wc<Wc>kNm3.obj` | Indexed triangular OBJ mesh in metres, using the same validated mesh topology as STL. |
| `antifer_<geometry>_<W>kN_Wc<Wc>kNm3.dxf` | AutoCAD 2018 / AC1032 DXF with one ACIS-backed `3DSOLID`, intended for CAD inspection and MASSPROP-type interrogation. |
| `output.txt` | Plain-text calculation, dimensional and validation report matching the GUI preview. |

All exported geometry is dimensional and written in metres. The exported XY origin is placed at the homogeneous centre of mass, while the exported Z datum remains the physical bottom level $z=0$.

## Hydraulic Stability, Structural Stability and Failure Modes

Antifer design practice falls within the tradition of the classic and universally accepted Hudson formula and subsequent extensions for artificial-unit armour layers. In typical form:

$$W = \frac{\gamma_{r}H_{D}^{3}}{K_{D}\left( S_{r} - 1 \right)^{3}\cot\alpha}$$

where $W$ is the unit weight, $H_{D}$ the design wave height, $S_{r}$ the submerged relative density and $K_{D}$ the stability coefficient. The central problem for Antifer has never been to discover a single universal $K_{D}$, but rather to determine **which** $K_{D}$ **is consistent with the placement method, admissible damage and type of wave action considered**. This is the common basis of modern Antifer stability interpretation and preliminary armour sizing.

### Comparative Stability Results

**Hydraulic-test conditions**

| Reference | Slope / regime | Placement |
|---|---|---|
| **Pita 1986** | $1:1,5$ to $1:2,0$ | not explicitly detailed here |
| **Rock Manual 2007** | two layers; ~5% damage | irregular |
| **Yagci 2004** | $\cot\alpha = 1,25$ to 2.5 | irregular |
| **Yagci 2004** | same test series | irregular |
| **Frens 2007** | $1:1,5$; irregular JONSWAP | various patterns |
| **Freitas 2013** | $1:1,5$; irregular waves | regular 1; regular 2; semi-irregular |
| **LNEC** | two layers; irregular tests | regular vs irregular |

**Metrics, results and interpretation**

| Reference | Metric | Main result | Interpretation |
|---|---|---:|---|
| **Pita 1986** | $K_{D}$ Hudson | 7.6 to 14.1 | Portuguese historical range. |
| **Rock Manual 2007** | recommended $K_{D}$ | 7-8 | practical reference value. |
| **Yagci 2004** | $K_{D}$ at 3% damage | 2.69 to 3.52 | highly damage-criterion dependent. |
| **Yagci 2004** | wave-height parameter | $H_{s}$ best | best stability descriptor. |
| **Frens 2007** | $K_{D}$ | 4.1 to 23.7 | placement governs response. |
| **Freitas 2013** | suggested $K_{D}$ | 5.8; 4.0; 2.1 | regular stable; semi-irregular repairable. |
| **LNEC** | stability + overtopping | regular more stable | irregular lowers overtopping. |

Yagci adds a methodologically important result: under irregular placement, $H_{s}$ was the wave-height parameter that best characterised stability, outperforming $H_{1/10}$ and $H_{\max}$. The same investigation obtained an **average porosity of approximately 0.47** in the modified irregular placement technique. The choice of damage criterion is decisive: definitions that include **rocking and turning**, in addition to rolling and displacement, produce lower $K_{D}$ values than definitions based only on extraction or rolling.

The Portuguese campaigns corroborate the fundamental physics of the problem. The LNEC work concludes that, for the same placement density, the irregular mode is more unstable than the regular one, but also considerably more effective in reducing overtopping. LNEC estimates that, in the case studied, the stability obtained with irregular placement could be reproduced with regular placement and a block density 10-15% lower. Freitas, at IST, reinforces that regular patterns showed higher hydraulic stability than the semi-irregular pattern, but also higher reflection.

In addition to $K_{D}$, overtopping performance is relevant. The Rock Manual provides roughness factors $\gamma_{f}$ for overtopping-prediction methods; for **Antifer cube in two layers**, the reference value is of the order of **0.47** in the TAW method, placing the Antifer close to classic cubes and showing that, although rough and porous, it does not automatically offer an overtopping advantage when compared with more open arrangements or high-porosity monolayer units.

### Stability and Load-Bearing Capacity Analysis by Geometry

At the **hydraulic** level, small differences between documented Antifer geometric parametrisations should not be treated as decisive hydraulic-performance differences. The variation in $K_D$ imposed by placement method is much more important than the variation associated with minor dimensional interpretation. The stability criterion should therefore be formulated as follows: **adopt a range of** $K_D$ **dependent on the placement pattern, verify critical works by physical modelling and do not extrapolate results from one arrangement to another**.

At the structural level, the superiority of the Antifer over Dolos/Tetrapod lies in the absence of slender arms and in wide resistant sections. Scaravaglione, when reviewing historical cases, states that Antifer cubes were selected in Sines for their relatively good mechanical resistance, precisely because they do not expose the unit to critical levels of bending and tension such as those of slender units. The geometric indicators that matter most here — net width between grooves, web thickness, self-weight, corner robustness and degree of draft — are controlled by the same compact massive-unit morphology. The practical consequence is clear: control of placement and execution parameters is more important than minor differences between dimensional parametrisations of the Antifer geometry.

### Failure Modes and Degradation Mechanisms

The relevant failure modes for Antifer units can be grouped into five families.

The first is **elementary hydraulic instability**: rocking, settling, turning, rolling and displacement. Yagci explicitly treats these movements in the damage definition; Frens observes that the first displacements typically occur around **SWL ± 5** $D_{n}$, highlighting the breaking zone and the zone of alternating submergence/emergence as the most critical.

The second is chain failure of the arrangement. In dense regular patterns, Frens notes that a single displaced block may induce a chain reaction, so his stability assessment for certain regular arrangements is based on zero displacements. This shows an important paradox: a very stable arrangement may, after the threshold has been exceeded, fail more abruptly.

The third is degradation by smoothing/paving. The Rock Manual had already warned of the risk of “face-to-face rearrangement”; Jensen returns to the criticism in a modern context, observing a tendency of some Antifer armour layers to self-orient and form a kind of relatively smooth “pavement”, which tends to increase run-up and overtopping. This is one of the persistent controversies of the unit.

The fourth is structural degradation of the concrete: cracking of thermal or shrinkage origin, lifting damage, impacts during transport/placement and corner abrasion. In the case of the Antifer, these risks exist, but are less critical than in thin-armed units. For this reason, manuals recommend low-heat-of-hydration concrete and careful curing.

The fifth is systemic failure through interaction with overtopping and the rear side. Frens documents that, in the most energetic series, overtopping could move material from the unprotected core on the rear side, creating a berm profile on the sheltered side. This reinforces that verification of the armour layer cannot be isolated from verification of the breakwater body, toe and crest.

## Manufacture, Materials, Testing and Quality Control

The manufacture of Antifer units was historically appreciated because it is much simpler than that of many modern interlocking units. The Rock Manual recommends, for the classic unit, unreinforced concrete, normally C25/30, consistency S2, with low heat of hydration because of the large thicknesses of the unit. The text also refers to a typical production rate of one unit per day and per mould, on a simple horizontal surface, using four-face formwork joined at the corners.

Frens adds a valuable operational detail: metal moulds open at the top and bottom, heavy enough not to lift due to negative pressure on the inclined faces; casting from the top; vibration; demoulding by vertical lifting of the mould; and prolonged moist curing. In the Brunei production case, the units were covered with hessian, kept moist, mobilised after 3 days and stored for at least another 27 days. This sequence is extremely consistent with the structural objective of the Antifer: avoiding thermal cracking and early damage in massive units.

### Materials and Relevant Properties

| Aspect | Reported value / practice | Note |
|---|---|---|
| Material type | plain concrete, normally unreinforced | Rock Manual |
| Usual class | C25/30 | Rock Manual |
| Consistency | S2 | Rock Manual |
| Heat of hydration | low | recommended for thick units |
| Typical model density | ~2450 kg/m³ | Freitas sample |
| Special high-density concretes | 25.4-32 kN/m³ in Portuguese projects; 3.1 t/m³ in Sines | Portuguese and Sines documentation |
| Reinforcement | generally absent | consistent with a massive unit |
| Critical control | thermal/shrinkage cracking, handling damage, density | essential for load-bearing capacity |

### Testing Protocols

Antifer units have been and continue to be studied mainly in **Froude physical models**. Freitas used the IST wave flume, slope $1:1,5$, irregular wave action, $T_{p} = 1,4$ s and significant wave-height series from 10 to 18 cm, with 13 tests in total. Frens used a 40 m by 0.80 m by 1.00 m flume, slope $1:1,5$, irregular JONSWAP waves, eight series of 1000-1500 waves, and fully reconstructed the armour layer between tests. Yagci combined regular and irregular waves, testing several slopes up to $\cot\alpha = 2,5$.

The performance indicators used in these studies include:

| Indicator | Use |
|---|---|
| $K_{D}$ Hudson | preliminary sizing and comparison between studies. |
| Porosity / packing density | relationship between armour openness and stability. |
| Number of displaced blocks | direct damage criterion. |
| $N_{od}$ or damage percentage | criterion for comparison between failure states. |
| Reflection coefficient $C_{r}$ | global hydrodynamic assessment. |
| Overtopping volume | functional performance of the breakwater. |
| Photographic observation / overlay | detection of individual movements. |
| Spatial reference $SWL \pm 5D_{n}$ | critical damage-counting zone. |

The combination of these indicators is particularly important for the Antifer because the unit may appear “stable” in terms of absence of massive block removal and yet have unfavourable functional performance in reflection and overtopping. It is exactly this tension between stability and functionality that explains the persistence of the regular versus irregular discussion.

## Case Studies, Standards, Patents and Controversies

### Representative Applications

Antifer units have been selected in several types of maritime works: first prototype development, severe-exposure repair, rehabilitation after armour-layer failure, full-scale monitoring, modern port-extension works and Atlantic island reconstruction.

| Case | Main technical role | Engineering relevance |
|---|---|---|
| **Port of Antifer** | genesis and first prototype application | origin of the grooved tapered cube concept. |
| **Sines West Breakwater** | post-Dolos emergency works and definitive rehabilitation | robust massive units selected after structural failure of slender Dolosse. |
| **Zeebrugge** | prototype overtopping and run-up measurements | real-scale functional data for grooved cube armour. |
| **Douro Bar / Cabedelo do Douro** | high-density Antifer use, model studies and monitoring | Portuguese case linking design, physical modelling and post-storm assessment. |
| **Leixões Outer Breakwater** | modern extension works with large Antifer blocks | contemporary Portuguese use in port-expansion works. |
| **Lajes das Flores** | emergency protection and reconstruction after extreme storm damage | recent Atlantic island-port resilience case. |
| **Mohammedia** | exposed international breakwater application | example of use under severe wave exposure. |
| **Brunei** | manufacture, curing and demoulding practice | useful construction-methodology example. |
| **Ponta Delgada** | rehabilitation context | Portuguese Atlantic-port application. |

Sines is the most didactic structural case. After the Dolos failure, Antifer units were used as a robust massive-unit solution in emergency and rehabilitation works. Zeebrugge is the most relevant full-scale functional case because prototype overtopping measurements were performed on a breakwater protected with grooved Antifer cubes. The Portuguese cases of the Douro Bar, Leixões and Lajes das Flores show that the Antifer remains a practical option for design, rehabilitation and emergency response in Atlantic port works.

### Standards and Reference Documents

| Document | Status | Contribution |
|---|---|---|
| **BS 6349-7** | British guide | CAU sizing and design framework. |
| **Rock Manual C683** | international manual | unit description, manufacture and dimensions. |
| **USACE CEM** | official USACE manual | general CAU practice. |
| **LNEC / IST** | Portuguese research | stability, overtopping and placement. |
| **Yagci / Frens** | academic research | placement-method effects. |

### Patents and Intellectual Property

The classic Antifer was not protected by an operational patent regime comparable to those of many modern monolayer units. This helped its diffusion, but also contributed to fragmented practices, moulds and placement arrangements.

There is, however, a later patent relevant to the history of the “grooved cube”: ES2385696, which claims an artificial cubic or parallelepiped unit with circular-section grooves along the symmetry axes of the faces, suitable for protection layers of dykes and banks. That patent, from 2008/2012, is related, but should not be confused with the canonical Antifer: it describes a broader family of grooved blocks, including units with grooves on all six faces, whereas the classic Antifer is described in manuals as a unit with four lateral grooves.

### Persistent Technical Controversies

| Controversy | Technical issue | Practical consequence |
|---|---|---|
| Stability versus function | $K_{D}$ gain can increase reflection and overtopping. | objective-dependent selection. |
| Economy | more concrete than many monolayer units. | robustness is bought with volume. |
| Morphological evolution | surface may become smoother or paved. | roughness loss and higher overtopping. |
| Unit-selection logic | no universal decision tree exists. | designer judgement remains decisive. |

The main controversy is the compromise between **stability** and **functional performance**. The Portuguese and Dutch studies are notably consistent: regular arrangements tend to produce higher $K_{D}$ values, but frequently with greater reflection and overtopping; irregular arrangements reduce these effects, but sacrifice armour-layer stability. This means that **the “best Antifer” does not exist outside a context of design objectives**.

The second controversy is economic. Antifer units consume more concrete than modern monolayer units. The price of that penalty is paid for greater structural robustness and lower sensitivity to bending failure.

The third controversy is morphological: the tendency of some Antifer armour layers to evolve into relatively smooth or “paved” surfaces, reducing effective roughness. This criticism appears in different forms in the Rock Manual and in more recent authors, and helps explain why the unit, despite its robustness, did not dominate the evolution of CAUs in the same way as certain patented monolayer solutions.

The fourth controversy is methodological: the sector does not have a universal objective decision tree for selecting the best concrete armour unit. The Antifer therefore remains a robustly prudent choice rather than a universal optimisation.

## Conclusions

The Pita Antifer geometry described here is defined by a compact algebraic model: a square frustum, four lateral plan chamfers and four identical circular side grooves. The adopted values are $A/H=1.086000$, $B/H=1.005000$, $D/H=0.024000$ and $r=R/H=0.121500$, with no top bevel and with $B$ measured directly at the actual top plane $z=H$.

The complete volume balance is:

$$
\frac{V}{H^3}
=\frac{a^2+ab+b^2}{3}-2d^2-4A_g.
$$

For the Pita values implemented in the script:

$$
\frac{a^2+ab+b^2}{3}=1.093617,
\qquad
2d^2=0.001152,
\qquad
4A_g=0.067765,
$$

and therefore:

$$
\frac{V}{H^3}=1.093617-0.001152-0.067765=1.024700.
$$

The groove is volume-consistent because the one-groove circular-segment area is solved from the historical volume coefficient. This gives $e=E/H=0.025906459609863$, $q/H=0.118705961731004$ and a generated circular-arc depth $c_{\mathrm{arc}}=0.095593540390137$, very close to the historical reported value $C/H=0.095600$.

For design purposes, the geometry definition does not remove the need for project-specific hydraulic verification. Stability remains governed primarily by placement method, packing density, armour slope, damage criterion, storm duration, toe support, construction tolerances and wave climate. The present script should therefore be read as a reproducible geometric CAD/BIM definition of Antifer units under the selectable Pita (1986) and Carvalho (2026) dimensional conventions, not as a substitute for hydraulic model testing or established armour-stability design practice.

## Python Script Installation, Usage and Viewing

The accompanying Python script is a Tkinter-based production tool for generating one dimensional Antifer armour-unit solid from the selected input weight $W$ and concrete unit weight $W_c$. It supports the Pita (1986) and Carvalho (2026) dimensional conventions and exports the same validated geometry to IFC, STL, OBJ and DXF.

### Script Purpose and Generated Deliverables

| Item | Script behaviour |
|---|---|
| Script type | Tkinter graphical production application |
| Geometry basis | pure vectorial generation; no embedded CAD, SAT, ACIS, IFC, DXF or mesh template |
| Selectable conventions | Carvalho (2026) and Pita (1986) |
| Input parameters | unit weight $W$ [kN] and concrete unit weight $W_c$ [kN/m³] |
| Volume formula | $V=W/W_c$ |
| Height formula | $H=(V/K_{V,\mathrm{generated}})^{1/3}$, using the closed CAD/B-rep coefficient of the selected convention |
| Top convention | $B$ is the top width at construction level $z=H$ |
| Top bevel | none |
| Corner chamfers | lateral plan chamfers with coefficient $D/H$ |
| Groove profile | one circular arc per side, with radius $R$ and centre offset $E$ |
| Groove sampling | `GROOVE_ARC_POINTS = 144` |
| IFC output | IFC4 `IfcFacetedBrep` with property and quantity data |
| STL output | closed triangular mesh in metres |
| OBJ output | indexed triangular mesh in metres |
| DXF output | AutoCAD 2018 / AC1032 ACIS-backed `3DSOLID` |
| Text output | `output.txt` calculation and validation report |

### Dimensional Conventions Used by the Script

The script uses the same vectorial topology for Pita and Carvalho: two homologous horizontal sections, four lateral plan chamfers and four single circular-arc side grooves. The coefficient set changes with the selected convention.

| Coefficient | Pita (1986) | Carvalho (2026) |
|---|---:|---:|
| normalisation factor $f$ | $1.000000000000$ | $0.987874174182$ |
| $A/H$ | $1.086000000000$ | $1.072831353161$ |
| $B/H$ | $1.005000000000$ | $0.992813545052$ |
| $D/H$ | $0.024000000000$ | $0.023708980180$ |
| $R/H$ | $0.121500000000$ | $0.120026712163$ |
| $E/H$ | $0.025906459610$ | $0.025592322393$ |
| $C/H=R/H-E/H$ | $0.095593540390$ | $0.094434389770$ |
| generated CAD/B-rep $K_V$ | $1.024700000000$ | $1.000000000000$ |

Pita keeps the historical dimensional reference. Carvalho applies the common horizontal normalisation factor to the Pita-derived plan and groove ratios so that the generated CAD/B-rep relation becomes $V/H^3=1.000000$.

### Required Python Environment

Python 3.10 or newer is recommended. Tkinter must be available; on standard Windows Python installers, Tkinter is normally included.

Install the runtime packages with:

```bash
python -m pip install ezdxf trimesh pillow
```

`pillow` is recommended for broad Windows/PyInstaller compatibility with optional `ezdxf` drawing add-ons. PyInstaller is only required when building a standalone executable.

### Windows Virtual Environment Creation

From the folder containing the script, create a local virtual environment:

```powershell
py -m venv .venv
```

Activate the virtual environment:

```powershell
.\.venv\Scripts\activate
```

After activation, upgrade `pip`:

```powershell
python -m pip install --upgrade pip
```

Install the required packages:

```powershell
python -m pip install ezdxf trimesh pillow
```

For standalone executable compilation, also install PyInstaller:

```powershell
python -m pip install pyinstaller
```

### Running the Script

Run the graphical application with:

```bash
python script_final_production.py
```

The graphical workflow is:

1. Enter the Antifer weight $W$ [kN].
2. Enter the concrete unit weight $W_c$ [kN/m³].
3. Select Carvalho (2026) or Pita (1986).
4. Select the output folder.
5. Review the live calculation and validation preview.
6. Press **Generate IFC + STL + OBJ + DXF**.

The selected output folder receives the IFC, STL, OBJ, DXF and `output.txt` files. The filenames include the selected convention, input weight and concrete unit weight, for example:

```text
antifer_carvalho2026_500kN_Wc24kNm3.ifc
antifer_carvalho2026_500kN_Wc24kNm3.stl
antifer_carvalho2026_500kN_Wc24kNm3.obj
antifer_carvalho2026_500kN_Wc24kNm3.dxf
output.txt
```

### Viewing the Exported Files

The IFC file can be inspected in IFC/BIM viewers that support faceted B-rep geometry. The STL and OBJ files can be inspected in mesh viewers and CAD applications with mesh import support. The DXF file is intended for AutoCAD/ZWCAD-type CAD inspection as an ACIS-backed `3DSOLID`, including MASSPROP-type interrogation where supported.

ZWCAD is available from:

```text
https://www.zwsoft.com/
```

### Standalone Executable Compilation

A PyInstaller spec file is recommended for repeatable Windows production builds:

```powershell
pyi-makespec --onefile --windowed --name script --collect-all ezdxf script_final_production.py
pyinstaller --clean --noconfirm script.spec
```

The compiled executable is written to the `dist` folder.

## Dedication

This work is respectfully dedicated to the memory of **Carlos Alberto Roldão Maia Pita** (1950-2002), Portuguese civil engineer and specialist in maritime hydraulics and rubble-mound breakwater design. His LNEC *Memória n.º 670 — Dimensionamento Hidráulico do Manto Resistente de Quebra-Mares de Talude* remains an important technical reference for Portuguese maritime engineering and provides a key historical basis for the geometric interpretation of Antifer cubes.

## References

1. Pita, C. A. R. M. *Dimensionamento Hidráulico do Manto Resistente de Quebra-Mares de Talude*. Laboratório Nacional de Engenharia Civil, Memória n.º 670, Lisboa, 1986.
2. BSI. *BS 6349-7:1991 Maritime structures — Part 7: Guide to the design and construction of breakwaters*, with 2010 corrigenda.
3. CIRIA; CUR; CETMEF. *The Rock Manual: The use of rock in hydraulic engineering*, 2nd ed., 2007.
4. U.S. Army Corps of Engineers. *Coastal Engineering Manual*. Engineer Manual EM 1110-2-1100, U.S. Army Corps of Engineers, Washington, D.C., 6 volumes, 2002. Official USACE Publications repository.
5. Yagci, O.; Kapdasli, S.; Cigizoglu, H. K. “The stability of the antifer units used on breakwaters in case of irregular placement”, *Ocean Engineering*, 31, 1111-1127, 2004.
6. Frens, A. B. *The Impact of Placement Method on Antifer-block Stability*. MSc thesis, Delft University of Technology, 2007.
7. Neves, M. G.; Silva, L. G.; Reither, S. *Stability and overtopping of rubble-mound breakwaters: influence of the placement method and density of cubic blocks*. LNEC / PIANC Portugal.
8. Chegini, V.; Aghtouman, P. Hydraulic stability formulae for Antifer blocks, 2006.
9. Freitas, P. M. G. *Hydraulic Stability of Antifer Cubes: Physical Model Study*. MSc dissertation, Instituto Superior Técnico, 2013.
10. Scaravaglione, G.; Latham, J.-P.; Xiang, J.; Francone, A.; Tomasicchio, G. R. “Historical overview of the structural integrity of Concrete Armour Units”, 2022.
11. Edge, B. L.; Magoon, O. T.; et al. / ASCE-ICCE documentation on the rehabilitation of the West Breakwater of Sines and the use of high-density Antifer cubes.
12. Reis, M. T.; Fortes, C. J. E. M.; Neves, M. G.; et al. “Rehabilitation of Sines west breakwater: wave overtopping study”, *Proceedings of the Institution of Civil Engineers - Maritime Engineering*, 2011.
13. Troch, P.; De Rouck, J.; Van Damme, L. “Full-scale wave-overtopping measurements on the Zeebrugge rubble mound breakwater”, *Coastal Engineering*, 2004.
14. Geeraerts, J.; De Rouck, J.; Troch, P.; et al. “Effects of new variables on the overtopping discharge at steep rubble mound breakwaters: the Zeebrugge prototype case”, 2009.
15. Jensen, O. J. Historical syntheses on the evolution of armour units and recent observations on Antifer behaviour on highly exposed breakwaters, including references to Antifer, Mohammedia and Zeebrugge.
16. Luís, L.; Freire, S.; Barros, J.; Lopes, H.; Lemos, R.; Fortes, C.; Neves, G. “Estudos e projetos do prolongamento do quebra-mar exterior e das acessibilidades marítimas do Porto de Leixões”, PIANC Portugal / LNEC, 2022.
17. Teixeira Duarte. “Extension of the Outer Breakwater and Maritime Access Ways of Leixões Port”, project description with Antifer block quantities and classes.
18. Portos dos Açores / NRV-Norvia / PORTUS. Documentation on the emergency protection and reconstruction of the Port of Lajes das Flores after Hurricane Lorenzo and subsequent storm damage.

---