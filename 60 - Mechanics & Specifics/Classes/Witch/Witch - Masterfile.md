| Stat                           | Note                                                                                |
| ------------------------------ | ----------------------------------------------------------------------------------- |
| **Hit Dice**                   | d10                                                                                 |
| **Saving Throw Proficiencies** | Wisdom, Intelligence                                                                |
| **Skill Proficiencies**        | *Chose 3:* Arcana, Insight, Investigation, Perception, Medicine, History, Deception |
| **Weapon Proficiency**         | Simple Weapons                                                                      |
```dataviewjs
// 1. Establish environmental parameters
const currentClass = dv.current().file.name.split(" - ")[0]; // Extracts "Witch" from note name
const currentFolder = dv.current().file.folder;
const featuresPath = `"${currentFolder}/Features"`;

// 2. Harvest all lore and feature notes across the local directories
const featureNotes = dv.pages(featuresPath)
                       .where(p => p.class === currentClass && !p.file.name.endsWith(" - Config"));

// 3. Initialize the chronological timeline matrix
const chronologicalMatrix = {};
for (let i = 1; i <= 20; i++) {
    chronologicalMatrix[i] = [];
}

// 4. Distribute features into their respective level brackets
featureNotes.forEach(page => {
    let assignedLevels = [];
    if (page.level !== undefined && page.level !== null) {
        if (typeof page.level === "number") {
            assignedLevels.push(page.level);
        } else if (Array.isArray(page.level)) {
            assignedLevels = page.level.map(Number);
        } else {
            assignedLevels = String(page.level).split(",").map(x => Number(x.trim()));
        }
    }
    
    assignedLevels.forEach(lvl => {
        if (chronologicalMatrix[lvl]) {
            chronologicalMatrix[lvl].push(page);
        }
    });
});

// 5. Asynchronously compile the master dossier text
let masterManifest = `# DESIGN MANIFEST: ${currentClass.toUpperCase()}\n`;

for (let lvl = 1; lvl <= 20; lvl++) {
    const levelFeatures = chronologicalMatrix[lvl];
    if (levelFeatures.length === 0) continue;

    // Alphabetize features arriving at the same level milestone
    levelFeatures.sort((a, b) => a.file.name.localeCompare(b.file.name));
    
    masterManifest += `\n=========================================\n`;
    masterManifest += `CHARACTER LEVEL ${lvl}\n`;
    masterManifest += `=========================================\n`;
    
    for (const page of levelFeatures) {
        const subtypeHeader = page.subtype ? ` [Classification: ${page.subtype}]` : "";
        masterManifest += `\n### FEATURE: ${page.file.name}${subtypeHeader}\n\n`;
        
        try {
            // Pull the raw file contents from the vault disk
            const rawContent = await dv.io.load(page.file.path);
            
            // Cleanse the frontmatter blocks to deliver pure text to the AI
            const cleanContent = rawContent.replace(/^---[\s\S]*?---\n/, "").trim();
            
            masterManifest += cleanContent + "\n\n";
        } catch (err) {
            masterManifest += `*Error reading feature source file at ${page.file.path}*\n\n`;
        }
        masterManifest += `\n-----------------------------------------\n`;
    }
}

// 6. Cast the final aggregated text document into an easily copied markdown frame
dv.paragraph("```markdown\n" + masterManifest + "\n```");
```
