> [!quote] "The world is set in two, the Grael, and the Tuatha, the world of body... and the world of spirit"

## Overview
The ever-shifting infinite, the vast [[Nameless]] that is both undefined in places and in others constant, the endless discovery and pathfinding as well as endless change. That is the world of [[Spirits]], where terrain shifts and changes constantly, where the beasts speak mortal tongues and have lessons older then some aspects. 

Here does dwell [[The Koutetuji]], [[The House of Empty]], [[Faekin]] together with their courts and many of the [[Aspect]] of [[Tuatha]]. 


```dataviewjs
let targetName = "Spirit World";
let folderPath = "Tale of The Last Cycle/Timeline";
let results = [];

// This grabs every page inside the "Timeline" folder
let pages = dv.pages(`"${folderPath}"`);

for (let page of pages) {
    let file = app.vault.getAbstractFileByPath(page.file.path);
    let cache = app.metadataCache.getFileCache(file);
    if (!cache || !cache.links) continue;

    // Search for any link that points to the Spirit World
    let spiritLinks = cache.links.filter(l => l.link === targetName || l.link.includes(targetName));
    let headers = cache.headings || [];
    
    let seenHeaders = new Set();

    for (let link of spiritLinks) {
        let closestHeader = "Top of File";
        for (let i = headers.length - 1; i >= 0; i--) {
            if (headers[i].position.start.line < link.position.start.line) {
                closestHeader = headers[i].heading;
                break;
            }
        }
        
        if (!seenHeaders.has(closestHeader)) {
            let cleanLink = "[[" + page.file.name + "#" + closestHeader + "]]";
            results.push([page.file.link, cleanLink]);
            seenHeaders.add(closestHeader);
        }
    }
}

dv.table(["Source Age", "Unique Event Gateways"], results);
```

