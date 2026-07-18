---
class: Witch
---

## Witch

#### Core Design
Witch features will gravitate towards triggering different reactions from the Stygian, an attack from the Witch will cause the Stygian to attack the same enemy. 

The basic idea is to create an weaving gameplay between Stygian and the Witch. 

| Stat                           | Note                                                                                |
| ------------------------------ | ----------------------------------------------------------------------------------- |
| **Hit Dice**                   | d10                                                                                 |
| **Saving Throw Proficiencies** | Wisdom, Intelligence                                                                |
| **Skill Proficiencies**        | *Chose 3:* Arcana, Insight, Investigation, Perception, Medicine, History, Deception |
| **Weapon Proficiency**         | Simple Weapons                                                                      |
```dataviewjs
// 1. The Core Spellcasting Timeline (Indexed by Effective Caster Level)
const masterSlotMatrix = {
    1:  [2, 0, 0, 0, 0, 0, 0, 0, 0],
    2:  [3, 0, 0, 0, 0, 0, 0, 0, 0],
    3:  [4, 2, 0, 0, 0, 0, 0, 0, 0],
    4:  [4, 3, 0, 0, 0, 0, 0, 0, 0],
    5:  [4, 3, 2, 0, 0, 0, 0, 0, 0],
    6:  [4, 3, 3, 0, 0, 0, 0, 0, 0],
    7:  [4, 3, 3, 1, 0, 0, 0, 0, 0],
    8:  [4, 3, 3, 2, 0, 0, 0, 0, 0],
    9:  [4, 3, 3, 3, 1, 0, 0, 0, 0],
    10: [4, 3, 3, 3, 2, 0, 0, 0, 0],
    11: [4, 3, 3, 3, 2, 1, 0, 0, 0],
    12: [4, 3, 3, 3, 2, 1, 0, 0, 0],
    13: [4, 3, 3, 3, 2, 1, 1, 0, 0],
    14: [4, 3, 3, 3, 2, 1, 1, 0, 0],
    15: [4, 3, 3, 3, 2, 1, 1, 1, 0],
    16: [4, 3, 3, 3, 2, 1, 1, 1, 0],
    17: [4, 3, 3, 3, 2, 1, 1, 1, 1],
    18: [4, 3, 3, 3, 3, 1, 1, 1, 1],
    19: [4, 3, 3, 3, 3, 2, 1, 1, 1],
    20: [4, 3, 3, 3, 3, 2, 2, 1, 1]
};

// All available spell tiers in the system
const allSpellHeaders = ["1st", "2nd", "3rd", "4th", "5th", "6th", "7th", "8th", "9th"];

// 2. Gather environmental variables and configuration data
const currentClass = dv.current().file.name;
const currentFolder = dv.current().file.folder;
const featuresPath = `"${currentFolder}/Features"`;
const configFilePath = `${currentFolder}/Features/${currentClass} - Config`;

const configPage = dv.page(configFilePath);
const casterType = String(configPage?.spellcaster || "none").toLowerCase().trim();
const progressionTracks = configPage?.progression || {};
const trackNames = Object.keys(progressionTracks);

// 3. Determine the mathematical limits of the caster's profile
let maxSlotTier = 0;
if (casterType === "full") maxSlotTier = 9;
else if (casterType === "half") maxSlotTier = 5;
else if (casterType === "third") maxSlotTier = 4;

const activeSpellHeaders = allSpellHeaders.slice(0, maxSlotTier);

// 4. Harvest and sort class feature files (recursively gathering from subfolders)
const featureNotes = dv.pages(featuresPath)
                       .where(p => p.class === currentClass && !p.file.name.endsWith(" - Config"));

const classMatrix = {};
for (let lvl = 1; lvl <= 20; lvl++) { classMatrix[lvl] = []; }

featureNotes.forEach(page => {
    let assignedLevels = [];
    if (page.level !== undefined && page.level !== null) {
        if (typeof page.level === "number") assignedLevels.push(page.level);
        else if (Array.isArray(page.level)) assignedLevels = page.level.map(Number);
        else assignedLevels = String(page.level).split(",").map(x => Number(x.trim()));
    }
    assignedLevels.forEach(lvl => {
        if (classMatrix[lvl]) {
            const hasUniqueSubtype = page.subtype && page.subtype.toLowerCase() !== "core";
            const displayString = hasUniqueSubtype ? `${page.file.link} (${page.subtype})` : page.file.link;
            classMatrix[lvl].push({ name: page.file.name, display: displayString });
        }
    });
});

// 5. Build rows dynamically using progression division formulas
const tableRows = [];

for (let lvl = 1; lvl <= 20; lvl++) {
    classMatrix[lvl].sort((a, b) => a.name.localeCompare(b.name));
    const featuresList = classMatrix[lvl].length > 0 ? classMatrix[lvl].map(f => f.display).join(", ") : "—";
    
    // Position 1 & 2: Level > Class Features
    const rowData = [lvl, featuresList];
    
    // Position 3: Configuration Tracks (Custom manual progression lines added next)
    trackNames.forEach(trackName => {
        const intervals = progressionTracks[trackName];
        const definedLevels = Object.keys(intervals).map(Number).sort((a, b) => a - b);
        let effectiveLevel = definedLevels[0];
        for (let dLvl of definedLevels) {
            if (lvl >= dLvl) effectiveLevel = dLvl;
            else break;
        }
        rowData.push(intervals[effectiveLevel] || "—");
    });
    
    // Position 4: Arcane Spellcasting Columns (Calculated with streamlined 2024 math)
    if (maxSlotTier > 0) {
        let ecl = 0;
        if (casterType === "full") {
            ecl = lvl;
        } else if (casterType === "half") {
            // 2024 Rule: Round up Level / 2 (Level 1 & 2 = ECL 1)
            ecl = Math.ceil(lvl / 2);
        } else if (casterType === "third") {
            // 2024 Rule: Round up Level / 3 (Level 1, 2, & 3 = ECL 1)
            ecl = Math.ceil(lvl / 3);
        }
        
        const levelSlots = masterSlotMatrix[ecl] || [0, 0, 0, 0, 0, 0, 0, 0, 0];
        const activeSlots = levelSlots.slice(0, maxSlotTier);
        
        activeSlots.forEach(slotCount => {
            rowData.push(slotCount > 0 ? slotCount : "—");
        });
    }
    
    tableRows.push(rowData);
}

// 6. Output the clean, dynamically bounded table framework
const tableHeaders = ["Level", "Class Features", ...trackNames, ...activeSpellHeaders];
dv.table(tableHeaders, tableRows);
```
```dataviewjs
// Anchor the master engine component context at the absolute summit
const componentInstance = this;
const { MarkdownRenderer } = require("obsidian");

// 1. Fetch your Witch feature notes, casting a protective filter to ignore configuration profiles
const rawPages = dv.pages('"60 - Mechanics & Specifics/Classes/Witch/Features"')
                   .where(p => p.class === "Witch" && !p.file.name.endsWith(" - Config"));

// Apply the multi-tier chronological level and alphabetical sorting array
const pages = rawPages.array().sort((a, b) => {
    const parseLevel = (p) => {
        if (!p.level) return 0;
        if (typeof p.level === "number") return p.level;
        if (Array.isArray(p.level)) return Number(p.level[0]) || 0;
        const firstTier = String(p.level).split(",")[0].trim();
        return Number(firstTier) || 0;
    };

    const levelA = parseLevel(a);
    const levelB = parseLevel(b);

    if (levelA !== levelB) {
        return levelA - levelB;
    }
    return a.file.name.localeCompare(b.file.name);
});

if (pages.length === 0) {
    dv.paragraph("No Witch features found within the specified archives.");
} else {
    // Encapsulate execution within a defensive asynchronous framework block
    (async () => {
        // Helper function to strip YAML properties and the very first header line
        const cleanFeatureContent = (raw) => {
            if (!raw) return "";
            let content = raw.replace(/^---[\s\S]*?---\s*/m, "");
            content = content.replace(/^#+\s+.*?\n/m, "");
            return content.trim();
        };

        // 2. Construct the master container viewport
        const container = dv.el("div", "");
        container.style.border = "1px solid var(--background-modifier-border)";
        container.style.borderRadius = "8px";
        container.style.padding = "25px";
        container.style.backgroundColor = "var(--background-secondary)";
        container.style.position = "relative";
        container.style.marginBottom = "20px";

        // 3. Forge the Navigation Control Deck with raw native HTML elements
        const controls = container.createDiv(); 
        controls.style.position = "relative";
        controls.style.display = "flex";
        controls.style.justifyContent = "space-between";
        controls.style.alignItems = "center";
        controls.style.marginBottom = "20px";
        controls.style.borderBottom = "1px solid var(--background-modifier-border)";
        
        // Spatial Realignment: ~0.2cm vertical (8px padding), ~0.5cm horizontal (20px padding)
        controls.style.margin = "-25px -25px 20px -25px";
        controls.style.padding = "8px 20px 12px 20px"; 
        controls.style.backgroundColor = "var(--background-secondary-alt)";
        controls.style.borderRadius = "8px 8px 0 0";

        const prevBtn = controls.createEl("button", { text: "◀ Prev" });
        
        const counter = controls.createEl("span", { text: `1 of ${pages.length}` });
        counter.style.fontSize = "0.85em";
        counter.style.color = "var(--text-muted)";
        counter.style.fontWeight = "bold";
        
        // Lock the counter to the mathematical dead center of the header bar
        counter.style.position = "absolute";
        counter.style.left = "50%";
        counter.style.transform = "translateX(-50%)";

        const nextBtn = controls.createEl("button", { text: "Next ▶" });

        let currentIndex = 0;
        const slides = [];

        // 4. Process and isolate each file's content beneath the controls
        for (let i = 0; i < pages.length; i++) {
            const page = pages[i];
            
            const slide = dv.el("div", "", { container: container });
            slide.style.display = i === 0 ? "block" : "none";
            
            // Render the primary interactive title link
            dv.header(2, page.file.link, { container: slide });
            
            // Technical metadata ribbon
            const metaLine = dv.el("p", "", { container: slide });
            metaLine.style.color = "var(--text-muted)";
            metaLine.style.fontSize = "0.85em";
            metaLine.style.borderBottom = "1px solid var(--background-modifier-border-focus)";
            metaLine.style.paddingBottom = "8px";
            
            const displayLevel = page.level ? page.level : "-";
            const displaySubtype = page.subtype ? page.subtype : "Class Feature";
            metaLine.innerHTML = `<strong>Level:</strong> ${displayLevel} | <strong>Subtype:</strong> ${displaySubtype}`;
            
            const contentDiv = dv.el("div", "", { container: slide });
            contentDiv.style.marginTop = "15px";

            // Defensive execution vault to prevent system crashes
            try {
                const rawContent = await dv.io.load(page.file.path);
                if (rawContent) {
                    const cleanContent = cleanFeatureContent(rawContent);
                    await MarkdownRenderer.render(app, cleanContent, contentDiv, page.file.path, componentInstance);
                } else {
                    contentDiv.innerHTML = "<p><em>The chronicle page appears empty.</em></p>";
                }
            } catch (err) {
                contentDiv.innerHTML = `<p style="color:var(--text-error)"><em>Failed to display body content: ${err.message}</em></p>`;
            }
            
            slides.push(slide);
        }

        // 5. Navigation Logic Engine
        function updateSlider(newIndex) {
            slides[currentIndex].style.display = "none";
            currentIndex = newIndex;
            slides[currentIndex].style.display = "block";
            counter.innerText = `${currentIndex + 1} of ${slides.length}`;
        }

        // 6. Bind interactive listeners to the control board
        prevBtn.addEventListener("click", () => {
            const targetIndex = (currentIndex - 1 + slides.length) % slides.length;
            updateSlider(targetIndex);
        });

        nextBtn.addEventListener("click", () => {
            const targetIndex = (currentIndex + 1) % slides.length;
            updateSlider(targetIndex);
        });
    })();
}
```

## Stygian

#### Core Design
Stygian is the react of the Witch, the second body that the player can move around the battlefield with its own action pool. However what stygian does is impacted by the Witch's turn. 

```dataviewjs
// Anchor the master engine component context at the absolute summit
const componentInstance = this;
const { MarkdownRenderer } = require("obsidian");

// 1. Fetch your Witch feature notes
const rawPages = dv.pages('"60 - Mechanics & Specifics/Classes/Witch/Features/Stygian"')
                   .where(p => p.class === "Witch");

// Apply the multi-tier chronological level and alphabetical sorting array
const pages = rawPages.array().sort((a, b) => {
    const parseLevel = (p) => {
        if (!p.level) return 0;
        if (typeof p.level === "number") return p.level;
        if (Array.isArray(p.level)) return Number(p.level[0]) || 0;
        const firstTier = String(p.level).split(",")[0].trim();
        return Number(firstTier) || 0;
    };

    const levelA = parseLevel(a);
    const levelB = parseLevel(b);

    if (levelA !== levelB) {
        return levelA - levelB;
    }
    return a.file.name.localeCompare(b.file.name);
});

if (pages.length === 0) {
    dv.paragraph("No Witch features found within the specified archives.");
} else {
    // Encapsulate execution within a defensive asynchronous framework block
    (async () => {
        // Helper function to strip YAML properties and the very first header line
        const cleanFeatureContent = (raw) => {
            if (!raw) return "";
            let content = raw.replace(/^---[\s\S]*?---\s*/m, "");
            content = content.replace(/^#+\s+.*?\n/m, "");
            return content.trim();
        };

        // 2. Construct the master container viewport
        const container = dv.el("div", "");
        container.style.border = "1px solid var(--background-modifier-border)";
        container.style.borderRadius = "8px";
        container.style.padding = "25px";
        container.style.backgroundColor = "var(--background-secondary)";
        container.style.position = "relative";
        container.style.marginBottom = "20px";

        // 3. Forge the Navigation Control Deck with raw native HTML elements
        const controls = container.createDiv(); 
        controls.style.position = "relative";
        controls.style.display = "flex";
        controls.style.justifyContent = "space-between";
        controls.style.alignItems = "center";
        controls.style.marginBottom = "20px";
        controls.style.borderBottom = "1px solid var(--background-modifier-border)";
        
        // Spatial Realignment: ~0.2cm vertical (8px padding), ~0.5cm horizontal (20px padding)
        controls.style.margin = "-25px -25px 20px -25px";
        controls.style.padding = "8px 20px 12px 20px"; 
        controls.style.backgroundColor = "var(--background-secondary-alt)";
        controls.style.borderRadius = "8px 8px 0 0";

        const prevBtn = controls.createEl("button", { text: "◀ Prev" });
        
        const counter = controls.createEl("span", { text: `1 of ${pages.length}` });
        counter.style.fontSize = "0.85em";
        counter.style.color = "var(--text-muted)";
        counter.style.fontWeight = "bold";
        
        // Lock the counter to the mathematical dead center of the header bar
        counter.style.position = "absolute";
        counter.style.left = "50%";
        counter.style.transform = "translateX(-50%)";

        const nextBtn = controls.createEl("button", { text: "Next ▶" });

        let currentIndex = 0;
        const slides = [];

        // 4. Process and isolate each file's content beneath the controls
        for (let i = 0; i < pages.length; i++) {
            const page = pages[i];
            
            const slide = dv.el("div", "", { container: container });
            slide.style.display = i === 0 ? "block" : "none";
            
            // Render the primary interactive title link
            dv.header(2, page.file.link, { container: slide });
            
            // Technical metadata ribbon
            const metaLine = dv.el("p", "", { container: slide });
            metaLine.style.color = "var(--text-muted)";
            metaLine.style.fontSize = "0.85em";
            metaLine.style.borderBottom = "1px solid var(--background-modifier-border-focus)";
            metaLine.style.paddingBottom = "8px";
            
            const displayLevel = page.level ? page.level : "-";
            const displaySubtype = page.subtype ? page.subtype : "Class Feature";
            metaLine.innerHTML = `<strong>Level:</strong> ${displayLevel} | <strong>Subtype:</strong> ${displaySubtype}`;
            
            const contentDiv = dv.el("div", "", { container: slide });
            contentDiv.style.marginTop = "15px";

            // Defensive execution vault to prevent system crashes
            try {
                const rawContent = await dv.io.load(page.file.path);
                if (rawContent) {
                    const cleanContent = cleanFeatureContent(rawContent);
                    await MarkdownRenderer.render(app, cleanContent, contentDiv, page.file.path, componentInstance);
                } else {
                    contentDiv.innerHTML = "<p><em>The chronicle page appears empty.</em></p>";
                }
            } catch (err) {
                contentDiv.innerHTML = `<p style="color:var(--text-error)"><em>Failed to display body content: ${err.message}</em></p>`;
            }
            
            slides.push(slide);
        }

        // 5. Navigation Logic Engine
        function updateSlider(newIndex) {
            slides[currentIndex].style.display = "none";
            currentIndex = newIndex;
            slides[currentIndex].style.display = "block";
            counter.innerText = `${currentIndex + 1} of ${slides.length}`;
        }

        // 6. Bind interactive listeners to the control board
        prevBtn.addEventListener("click", () => {
            const targetIndex = (currentIndex - 1 + slides.length) % slides.length;
            updateSlider(targetIndex);
        });

        nextBtn.addEventListener("click", () => {
            const targetIndex = (currentIndex + 1) % slides.length;
            updateSlider(targetIndex);
        });
    })();
}
```



