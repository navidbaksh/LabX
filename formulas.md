# LabX — Formula Sources & Scientific References

This document provides mathematical formulations, algorithmic implementations, and peer-reviewed literature references for calculations implemented in LabX.

---

## 1. Solutions & Concentrations

### 1.1 Dilution Formula
- **Equation**:
  $$C_1 V_1 = C_2 V_2 \implies V_1 = \frac{C_2 V_2}{C_1}$$
  $$V_{\text{diluent}} = V_2 - V_1$$
- **Serial Dilution**:
  $$C_i = C_0 \times (\text{DF})^i \quad \text{where } \text{DF} = \frac{V_{\text{transfer}}}{V_{\text{transfer}} + V_{\text{diluent}}}$$
- **Reference**: Skoog, D. A., West, D. M., Holler, F. J., & Crouch, S. R. (2013). *Fundamentals of Analytical Chemistry* (9th ed.). Cengage Learning.

### 1.2 Molar Mass & Buffer Preparation
- **Solid Solute Mass**:
  $$\text{Mass } (g) = M (\text{mol/L}) \times V (L) \times \text{MW} (\text{g/mol})$$
- **Overshoot Volume Adjustment**:
  If measured mass $m_{\text{actual}} > m_{\text{target}}$:
  $$V_{\text{adjusted}} = \frac{m_{\text{actual}}}{M_{\text{desired}} \times \text{MW}}$$
- **Henderson-Hasselbalch Equation** (pH buffer calculation):
  $$\text{pH} = \text{p}K_a + \log_{10} \left( \frac{[\text{A}^-]}{[\text{HA}]} \right)$$

---

## 2. Nucleic Acids & PCR

### 2.1 Oligonucleotide Melting Temperature ($T_m$)
Four complementary models are implemented:

1. **Wallace Rule** (short primers $< 14\text{ nt}$):
   $$T_m = 2 \times (A + T) + 4 \times (G + C)$$
   *Reference*: Wallace, R. B., et al. (1979). Hybridization of synthetic oligodeoxyribonucleotides to phi chi 174 DNA. *Nucleic Acids Research*, 6(11), 3543–3557.

2. **Marmur-Doty / Chester-Marshak Equation** (oligos $\ge 14\text{ nt}$):
   $$T_m = 64.9 + 41.0 \times \left( \frac{(G+C) - 16.4}{N} \right)$$
   *Reference*: Chester, N., & Marshak, D. R. (1993). dimethyl sulfoxide-mediated primer annealing. *Analytical Biochemistry*, 209(2), 284–290.

3. **Salt-Adjusted Model**:
   - DNA:
     $$T_m = 100.5 + 41.0 \times \left(\frac{G+C}{N}\right) - \frac{820}{N} + 16.6 \log_{10}[\text{Na}^+]$$
   - RNA:
     $$T_m = 79.8 + 18.5 \log_{10}[\text{Na}^+] + 58.4 f_{GC} + 11.8 f_{GC}^2 - \frac{820}{N}$$
   *Reference*: Schildkraut, C., & Lifson, S. (1965). Dependence of the melting temperature of DNA on salt concentration. *Biopolymers*, 3(2), 195–208.

4. **Nearest-Neighbor Thermodynamic Model**:
   $$T_m = \frac{\Delta H^\circ \times 1000}{\Delta S^\circ + R \ln(C_t / x)} - 273.15 + 16.6 \log_{10}[\text{Na}^+]$$
   where $R = 1.9872\text{ cal/(mol}\cdot\text{K)}$, $C_t$ is total strand concentration, $x = 4$ for non-self-complementary duplexes and $x = 1$ for self-complementary duplexes.
   *Parameters*:
   - DNA: SantaLucia, J. (1998). A unified view of polymer, dumbbell, and oligonucleotide DNA nearest-neighbor thermodynamics. *PNAS*, 95(4), 1460–1465.
   - RNA: Xia, T., et al. (1998). Thermodynamic parameters for an expanded nearest-neighbor model for formation of RNA duplexes. *Biochemistry*, 37(42), 14719–14735.

### 2.2 Oligonucleotide Extinction Coefficient ($\epsilon_{260}$)
Calculated using the nearest-neighbor sum:
$$\epsilon_{260} = \sum \epsilon_{\text{mononucleotide}}$$
- Values: $A = 15,200$, $G = 12,010$, $C = 7,050$, $T = 8,400$, $U = 9,800\text{ L/(mol}\cdot\text{cm)}$
- *Reference*: Cavaluzzi, M. J., & Borer, P. N. (2004). Revised UV extinction coefficients for nucleoside-5'-monophosphates and unpaired DNA. *Nucleic Acids Research*, 32(1), e13.

### 2.3 DNA/RNA Molecular Weight Formulas
Based on New England Biolabs (NEB) standards:
- **dsDNA**: $\text{MW} = (N_{\text{bp}} \times 615.94) + 36.04\text{ g/mol}$
- **ssDNA**: $\text{MW} = (N_{\text{nt}} \times 307.97) + 18.02\text{ g/mol}$
- **ssRNA**: $\text{MW} = (N_{\text{nt}} \times 320.47) + 18.02\text{ g/mol}$
- **dsRNA**: $\text{MW} = (N_{\text{bp}} \times 640.94) + 36.04\text{ g/mol}$
- **Terminal 5'-Monophosphate**: Add $+79.0\text{ g/mol}$.
- **Terminal 5'-Triphosphate** (in vitro transcription RNA): Add $+159.0\text{ g/mol}$.

### 2.4 Molar Copy Number
$$\text{Copy Number} = \text{Moles} \times N_A = \left( \frac{\text{Mass } (g)}{\text{MW } (g/\text{mol})} \right) \times 6.02214076 \times 10^{23}\text{ molecules/mol}$$
*Reference*: CODATA 2018 recommended value for Avogadro's constant.

### 2.5 Ligation Insert Mass
$$\text{Mass}_{\text{insert}} (\text{ng}) = \text{Molar Ratio} \times \text{Mass}_{\text{vector}} (\text{ng}) \times \left( \frac{\text{Length}_{\text{insert (bp)}}}{\text{Length}_{\text{vector (bp)}}} \right)$$

---

## 3. Spectroscopy & Photometry

### 3.1 Beer-Lambert Law
$$A = \epsilon \cdot c \cdot l \iff c = \frac{A}{\epsilon \cdot l}$$
- $A$: Absorbance (dimensionless unit, OD)
- $\epsilon$: Molar absorption coefficient ($\text{M}^{-1}\text{cm}^{-1}$)
- $c$: Analyte concentration ($\text{M}$)
- $l$: Optical path length ($1.0\text{ cm}$ standard)

### 3.2 Nucleic Acid Quantitation Factors ($A_{260}$)
With baseline turbidity subtraction $(A_{260} - A_{320})$:
- **dsDNA**: $1.0\ A_{260} = 50\ \mu\text{g/mL}$
- **ssDNA**: $1.0\ A_{260} = 33\ \mu\text{g/mL}$
- **ssRNA**: $1.0\ A_{260} = 40\ \mu\text{g/mL}$
- **Pure ratios**:
  - $A_{260}/A_{280} \approx 1.8$ (dsDNA), $\approx 2.0$ (RNA)
  - $A_{260}/A_{230} \approx 2.0 - 2.2$
*Reference*: Sambrook, J., & Russell, D. W. (2001). *Molecular Cloning: A Laboratory Manual* (3rd ed.). Cold Spring Harbor Laboratory Press.

---

## 4. Sequence & Alignment Algorithms

### 4.1 Needleman-Wunsch Global Alignment (EMBOSS Needle)
- **Score Matrix Recurrence**:
  $$H[i, j] = \max \begin{cases}
    H[i-1, j-1] + S(a_i, b_j) \\
    E[i, j] \\
    F[i, j]
  \end{cases}$$
- **Affine Gap Costs**:
  $$E[i, j] = \max(H[i, j-1] - gap_{\text{open}}, E[i, j-1] - gap_{\text{extend}})$$
  $$F[i, j] = \max(H[i-1, j] - gap_{\text{open}}, F[i-1, j] - gap_{\text{extend}})$$
- **Substitution Matrices**:
  - Protein: **BLOSUM62** (*Henikoff & Henikoff, 1992, PNAS*, 89(22), 10915–10919).
  - Nucleic acids: **EDNAFULL** (EMBOSS standard nucleotide matrix).
- *Reference*: Needleman, S. B., & Wunsch, C. D. (1970). A general method applicable to the search for similarities in the amino acid sequence of two proteins. *JMB*, 48(3), 443–453.

---

## 5. Protein Physicochemical Properties (ProtParam)

### 5.1 Extinction Coefficient ($\epsilon_{280}$)
Based on tryptophan, tyrosine, and cystine content:
$$\epsilon_{\text{reduced}} = 5500 \times N_{\text{Trp}} + 1490 \times N_{\text{Tyr}}$$
$$\epsilon_{\text{oxidized}} = 5500 \times N_{\text{Trp}} + 1490 \times N_{\text{Tyr}} + 125 \times N_{\text{Cystine}}$$
*Reference*: Pace, C. N., et al. (1995). How to measure and predict the molar absorption coefficient of a protein. *Protein Science*, 4(11), 2411–2423.

### 5.2 Theoretical Isoelectric Point ($pI$)
Determined by finding root $\text{pH}$ where net charge $Q(\text{pH}) = 0$:
$$Q(\text{pH}) = \sum_{i=1}^{N_{\text{basic}}} \frac{1}{10^{\text{pH} - pK_{a, i}} + 1} - \sum_{j=1}^{N_{\text{acidic}}} \frac{1}{10^{pK_{a, j} - \text{pH}} + 1}$$
*Reference*: Bjellqvist, B., et al. (1993). The focusing positions of polypeptides in immobilized pH gradients can be predicted from their amino acid sequences. *Electrophoresis*, 14(1), 1023–1031.

### 5.3 Instability Index ($II$)
$$II = \frac{10}{L} \sum_{i=1}^{L-1} \text{DIWV}(x_i, x_{i+1})$$
A protein with $II < 40$ is predicted as stable in vitro; $II > 40$ is predicted as unstable.
*Reference*: Guruprasad, K., Reddy, B. V., & Pandit, M. W. (1990). Correlation between stability of a protein and its dipeptide composition. *Protein Engineering*, 4(2), 155–161.

### 5.4 Aliphatic Index ($AI$)
$$AI = \frac{100}{L} \left( N_{\text{Ala}} + 2.9 \times N_{\text{Val}} + 3.9 \times (N_{\text{Ile}} + N_{\text{Leu}}) \right)$$
*Reference*: Ikai, A. (1980). Thermostability and aliphatic index of globular proteins. *J. Biochem.*, 88(6), 1895–1898.

### 5.5 GRAVY (Grand Average of Hydropathicity)
$$\text{GRAVY} = \frac{1}{L} \sum_{i=1}^L \text{Hydropathy}(aa_i)$$
*Reference*: Kyte, J., & Doolittle, R. F. (1982). A simple method for displaying the hydropathic character of a protein. *JMB*, 157(1), 105–132.

### 5.6 Ammonium Sulfate Precipitation
Solid salt required to raise saturation from $S_1$ to $S_2$:
$$G = V (L) \times \frac{\text{SatG} \times (S_2 - S_1)}{\text{SatM} - \left( \frac{\bar{v}}{1000} \times \text{MW} \times \text{SatM} \times S_2 \right)}$$
where $\text{MW} = 132.14\text{ g/mol}$ and specific volume $\bar{v} = 0.54\text{ mL/g}$.
*Reference*: Green, A. A., & Hughes, W. L. (1955). Protein fractionation on the basis of solubility in aqueous solutions of salts and organic solvents. *Methods in Enzymology*, 1, 67–90.

---

## 6. Biophysical Curve Fitting (Levenberg-Marquardt)

Iterative damped least-squares minimization of:
$$\chi^2(p) = \sum_{i=1}^N \left( \frac{y_i - f(x_i, p)}{\sigma_i} \right)^2$$
Solving:
$$(J^T J + \lambda \operatorname{diag}(J^T J)) \Delta p = J^T r$$

1. **EMSA (Hill Equation)**:
   $$Y = \text{Bottom} + \frac{\text{Top} - \text{Bottom}}{1 + (K_d / X)^h}$$
2. **Fluorescence Polarization (Quadratic Binding)**:
   $$[RL] = \frac{(R_T + L_T + K_d) - \sqrt{(R_T + L_T + K_d)^2 - 4 R_T L_T}}{2}$$
   $$\text{Anisotropy } r = r_0 + (r_{\text{max}} - r_0) \frac{[RL]}{L_T}$$
3. **ITC (Wiseman Isotherm)**:
   Fits stoichiometric ratio $n$, binding constant $K_a = 1/K_d$, and enthalpy $\Delta H$.
   $$\Delta G = -R T \ln(K_a), \quad \Delta S = \frac{\Delta H - \Delta G}{T}$$
*Reference*: Levenberg, K. (1944). *Quarterly of Applied Mathematics*, 2(2), 164–168; Marquardt, D. W. (1963). *SIAM J. Appl. Math.*, 11(2), 431–441.

---

## 7. Biodiversity & Ecological Metrics

- **Shannon Diversity Index ($H'$)**:
  $$H' = -\sum_{i=1}^S p_i \ln(p_i) \quad \text{where } p_i = \frac{n_i}{N}$$
  *Reference*: Shannon, C. E. (1948). A mathematical theory of communication. *Bell System Technical Journal*, 27(3), 379–423.

- **Pielou's Evenness ($J'$)**:
  $$J' = \frac{H'}{\ln(S)}$$
  *Reference*: Pielou, E. C. (1966). The measurement of diversity in different types of biological collections. *Journal of Theoretical Biology*, 13, 131–144.

- **Simpson's Diversity**:
  - Dominance $D = \sum_{i=1}^S p_i^2$
  - Gini-Simpson Index $= 1 - D$
  - Reciprocal Simpson $= 1 / D$
  *Reference*: Simpson, E. H. (1949). Measurement of diversity. *Nature*, 163, 688.

- **Berger-Parker Dominance Index ($d$)**:
  $$d = \frac{\max(n_i)}{N}$$
  *Reference*: Berger, W. H., & Parker, F. L. (1970). Diversity of planktonic foraminifera in deep-sea sediments. *Science*, 168(3937), 1345–1347.

---

## 8. Microscopy & Cell Culture

### 8.1 Cell Culture Doubling Time
$$t_d = t \times \frac{\ln(2)}{\ln(N_t / N_0)}$$

### 8.2 Micrograph Scale Calibration
$$\text{Physical Scale } (\mu\text{m/pixel}) = \frac{\text{Camera Sensor Pixel Pitch } (\mu\text{m})}{\text{Objective Magnification} \times \text{Coupler Magnification}}$$
- Scale bar lengths are dynamically rounded to standard $1, 2, 5 \times 10^k$ step values representing approximately $15\% - 25\%$ of the field of view.
