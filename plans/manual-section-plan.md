# Manual Section Design Plan

## Overview
Add a "Manual" section below the calculator that explains how each calculation works. The section will contain three blocks corresponding to the three calculators.

## Location
The manual section will be placed after the main calculator grid (after line 252 in index.html) and before the footer (before line 254).

## Design Structure

### Main Container
- Full-width section with max-width matching the calculator grid (1400px)
- Centered with padding
- Consistent with existing design language

### Section Header
- Title: "Manual de Cálculo"
- Icon: `menu_book` or `help_outline`
- Optional: Subtitle explaining the purpose

### Three Manual Blocks (Cards)
Each block will be a card containing:

#### Block 1: Cálculo da Adição
- **Header**: Icon + Title "Cálculo da Adição" + Subtitle "Entradas: Longe e Perto"
- **Content Sections**:
  1. 📘 Manual Técnico
     - Explanation of the concept
     - Formula: `Adição = Perto − Longe`
     - Example calculation
  2. ℹ️ Tooltip (styled as an info box)
     - Quick explanation
     - Example
  3. 🚀 Tela de Onboarding (styled as a tip box)
     - User guidance

#### Block 2: Cálculo da Dioptria de Perto
- **Header**: Icon + Title "Cálculo da Dioptria de Perto" + Subtitle "Entradas: Longe e Adição"
- **Content Sections**:
  1. 📘 Manual Técnico
     - Formula: `Perto = Longe + Adição`
     - Example calculation
  2. ℹ️ Tooltip
  3. 🚀 Tela de Onboarding

#### Block 3: Cálculo da Dioptria de Longe
- **Header**: Icon + Title "Cálculo da Dioptria de Longe" + Subtitle "Entradas: Perto e Adição"
- **Content Sections**:
  1. 📘 Manual Técnico
     - Formula: `Longe = Perto − Adição`
     - Example calculation
  2. ℹ️ Tooltip
  3. 🚀 Tela de Onboarding

## Styling Approach

### Color Scheme
- Primary color: `#f26b2b` (matching existing)
- Background: `bg-white dark:bg-slate-900`
- Border: `border-slate-200 dark:border-slate-800`
- Text: `text-slate-900 dark:text-white`

### Card Design
- Rounded corners: `rounded-xl`
- Shadow: `shadow-sm`
- Border: `border border-slate-200 dark:border-slate-800`

### Section Styling
- Manual Técnico: White/light background with subtle border
- Tooltip: Light blue/primary tinted background (`bg-primary/5 dark:bg-primary/10`)
- Tela de Onboarding: Green/success tinted background (`bg-green-50 dark:bg-green-900/20`)
- Example Label: `text-sm font-medium text-slate-700 dark:text-slate-300` for consistent visual hierarchy

### Icons
- 📘: `menu_book` or `description`
- ℹ️: `info`
- 🚀: `rocket_launch` or `tips_and_updates`

## Interactive Features (Optional)

### Collapsible Sections
- Each manual block can be collapsed/expanded
- Chevron icon indicates state
- Saves space on mobile

### Copy Formula Button
- Click to copy formula to clipboard
- Visual feedback when copied

## Responsive Design
- Desktop: 3 columns (same as calculator)
- Tablet: 2 columns
- Mobile: 1 column (stacked)

## HTML Structure Example

```html
<section class="mt-12 max-w-[1400px] mx-auto px-4 lg:px-8" aria-labelledby="manual-calculo">
    <div class="flex items-center gap-3 mb-6">
        <span class="bg-primary/10 text-primary p-2 rounded-lg material-symbols-outlined" aria-hidden="true">menu_book</span>
        <h2 id="manual-calculo" class="text-2xl font-bold text-slate-900 dark:text-white">Manual de Cálculo</h2>
    </div>
    
    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <!-- Manual Block 1 -->
        <div class="bg-white dark:bg-slate-900 rounded-xl shadow-sm border border-slate-200 dark:border-slate-800">
            <!-- Header -->
            <div class="px-6 py-4 border-b border-slate-100 dark:border-slate-800">
                <h3 class="font-bold text-lg">Cálculo da Adição</h3>
                <p class="text-slate-500 text-sm">Entradas: Longe e Perto</p>
            </div>
            <!-- Content -->
            <div class="p-6 space-y-4">
                <!-- Manual Técnico -->
                <div class="p-4 bg-slate-50 dark:bg-slate-800/50 rounded-lg">
                    <h4 class="font-semibold flex items-center gap-2 mb-2">
                        <span>📘</span> Manual Técnico
                    </h4>
                    <p class="text-sm text-slate-600 dark:text-slate-300 mb-3">...</p>
                    <div class="bg-white dark:bg-slate-900 p-3 rounded border border-slate-200 dark:border-slate-700">
                        <p class="font-mono text-sm">Adição = Perto − Longe</p>
                    </div>
                </div>
                <!-- Tooltip -->
                <div class="p-4 bg-primary/5 dark:bg-primary/10 rounded-lg border border-primary/20">
                    <h4 class="font-semibold flex items-center gap-2 mb-2">
                        <span>ℹ️</span> Tooltip
                    </h4>
                    <p class="text-sm text-slate-600 dark:text-slate-300">...</p>
                </div>
                <!-- Tela de Onboarding -->
                <div class="p-4 bg-green-50 dark:bg-green-900/20 rounded-lg border border-green-200 dark:border-green-800">
                    <h4 class="font-semibold flex items-center gap-2 mb-2">
                        <span>🚀</span> Tela de Onboarding
                    </h4>
                    <p class="text-sm text-slate-600 dark:text-slate-300">...</p>
                </div>
            </div>
        </div>
        <!-- Manual Block 2 and 3 similar structure -->
    </div>
</section>
```

## Content Mapping

### Block 1: Cálculo da Adição
- **Manual Técnico**: A adição corresponde à diferença dióptrica entre a refração esférica para perto e para longe, sendo a principal característica da presbiopia. **Nota: A adição é sempre considerada um valor positivo na prescrição.**
- **Formula**: Adição = Perto − Longe
- **Example**: Longe: −2,00, Perto: +0,50 → Adição = +0,50 − (−2,00) = +2,50
- **Tooltip**: Calcula a adição subtraindo a dioptria de longe da dioptria de perto. Ex.: Perto +0,50 e Longe −2,00 → Adição +2,50
- **Onboarding**: Informe a dioptria de longe e a de perto para obter automaticamente o valor da adição, calculado pela diferença entre os dois valores.

### Block 2: Cálculo da Dioptria de Perto
- **Manual Técnico**: A dioptria de perto é obtida pela soma da refração de longe com o valor da adição prescrita. **Nota: considerar sempre a adição como valor positivo.**
- **Formula**: Perto = Longe + Adição
- **Example**: Longe: −1,50, Adição: +2,00 → Perto = −1,50 + 2,00 = +0,50
- **Tooltip**: Soma a dioptria de longe com a adição para encontrar a dioptria de perto. Ex.: −1,50 + 2,00 = +0,50
- **Onboarding**: Utilize este cálculo quando a receita informar longe e adição separadamente. O sistema retorna a dioptria correta para visão de perto.

### Block 3: Cálculo da Dioptria de Longe
- **Manual Técnico**: A dioptria de longe pode ser determinada subtraindo o valor da adição da refração de perto. **Nota: considerar sempre a adição como valor positivo.**
- **Formula**: Longe = Perto − Adição
- **Example**: Perto: +1,00, Adição: +2,50 → Longe = +1,00 − 2,50 = −1,50
- **Tooltip**: Subtraia a adição da dioptria de perto para obter a dioptria de longe. Ex.: +1,00 − 2,50 = −1,50
- **Onboarding**: Este cálculo é indicado quando a prescrição apresenta apenas a refração para perto e o valor da adição.
