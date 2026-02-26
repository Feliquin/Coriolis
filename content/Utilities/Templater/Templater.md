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
    "🌟 Information",
    'TABLE WITHOUT ID file.link AS Info FROM #info WHERE !contains(file.name, "Template") SORT file.name asc',
  ],
  [
    "🌟 Locations",
    'TABLE WITHOUT ID file.link AS Location FROM #location WHERE !contains(file.name, "Template") SORT file.name asc',
  ],
  [
    "📕 Log Book",
    'TABLE WITHOUT ID session AS "Session", file.link AS "Log entry" FROM #logentry WHERE !contains(file.name, "Template") SORT session asc, file.name asc',
  ],
  [
    "🎲 Meta",
    'TABLE WITHOUT ID file.link AS "Meta Fragment" FROM #meta WHERE !contains(file.name, "Template") SORT file.name asc',
  ],
  [
    "🌟 Ships",
    'TABLE WITHOUT ID file.link AS Ship FROM #ship WHERE !contains(file.name, "Template") SORT file.name asc',
  ],
  [
    "🌟 Contacts",
    'TABLE WITHOUT ID file.link AS Contact FROM #contact WHERE !contains(file.name, "Template") SORT file.name asc',
  ],
  [
    "🗒 Recently Added",
    'TABLE WITHOUT ID file.link AS Entry, dateformat(file.mtime, "ff") AS Added FROM #fragment WHERE !contains(file.name, "Template") SORT file.ctime desc LIMIT 20',
  ],
  [
    "🗒 Recently Edited",
    'TABLE WITHOUT ID file.link AS Entry, dateformat(file.mtime, "ff") AS Modified FROM #fragment WHERE !contains(file.name, "Template") SORT file.mtime desc LIMIT 20',
  ],
]);

await fileAndQuery.forEach(async (query, filename) => {

  const tFile = tp.file.find_tfile(filename);
  const queryOutput = await dv.queryMarkdown(query);

  // write query output to file
  await app.vault.modify(tFile, queryOutput.value);

});
%>