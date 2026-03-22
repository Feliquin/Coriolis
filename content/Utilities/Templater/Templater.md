---
creation date: <% tp.file.creation_date() %>
modification date: <% tp.file.last_modified_date("dddd Do MMMM YYYY HH:mm:ss") %>
tags:
  - utilitity
---
Updated:  <% tp.date.now("YYYY-MM-DD HH:mm:ss") %>

<%*
const dv = app.plugins.plugins["dataview"].api;

const fileAndQuery = new Map([
  [
    "⚠ DraftTemplate",
    'TABLE WITHOUT ID file.link AS Fragment FROM #fragment WHERE !contains(file.name, "Template") AND draft SORT file.name asc',
  ],  
  [
    "🌟 Information",
    'TABLE WITHOUT ID file.link AS Info, type AS Type FROM #info WHERE !contains(file.name, "Template") AND !draft SORT file.name asc',
  ],
  [
    "🌟 Locations",
    'TABLE WITHOUT ID file.link AS Location, type AS Type FROM #location WHERE !contains(file.name, "Template") AND !draft SORT file.name asc',
  ],
  [
    "📕 Log Book",
    'TABLE WITHOUT ID session AS "Session", file.link AS "Log entry", location as "Location", xp as "XP" FROM #logentry WHERE !contains(file.name, "Template") AND !draft SORT session desc, file.name asc',
  ],
  [
    "🎲 Meta",
    'TABLE WITHOUT ID file.link AS "Meta Fragment" FROM #meta WHERE !contains(file.name, "Template") AND !draft SORT file.name asc',
  ],
  [
    "🌟 Ships",
    'TABLE WITHOUT ID file.link AS Ship FROM #ship WHERE !contains(file.name, "Template") AND !draft SORT file.name asc',
  ],
  [
    "🌟 Contacts",
    'TABLE WITHOUT ID file.link AS Contact, status AS Status FROM #contact WHERE !contains(file.name, "Template") AND !draft SORT file.name asc',
  ],
  [
    "🗒 Recently Added",
    'TABLE WITHOUT ID file.link AS Entry, dateformat(file.mtime, "ff") AS Added FROM #fragment WHERE !contains(file.name, "Template") AND !draft SORT file.ctime desc LIMIT 20',
  ],
  [
    "🗒 Recently Edited",
    'TABLE WITHOUT ID file.link AS Entry, dateformat(file.mtime, "ff") AS Modified FROM #fragment WHERE !contains(file.name, "Template") AND !draft SORT file.mtime desc LIMIT 20',
  ],
]);

await fileAndQuery.forEach(async (query, filename) => {

  const tFile = tp.file.find_tfile(filename);
  const queryOutput = await dv.queryMarkdown(query);

  // write query output to file
  await app.vault.modify(tFile, queryOutput.value);

});
%>