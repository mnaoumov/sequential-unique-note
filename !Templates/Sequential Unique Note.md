<%*
const configFile = '.obsidian/sequential-unique-note.json';
const config = await app.vault.readJson(configFile) ?? { lastId: 0 };
const lastId = Number(config.lastId);
let nextId = lastId + 1;
if (Number.isNaN(nextId)) {
    nextId = 1;
}

while (await tp.file.exists(`${nextId}.md`)) {
	nextId++;
}

await tp.file.rename(String(nextId));
await app.vault.writeJson(configFile, { lastId: nextId });
%>