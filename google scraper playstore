import gplay from 'google-play-scraper';
import fs from 'fs/promises';
import Papa from 'papaparse';

(async () => {
  try {
    const inputCSVData = await fs.readFile('apps.csv', 'utf-8');
    const parsedCSVData = Papa.parse(inputCSVData, { header: true });
    const appRows = parsedCSVData.data;

    const outputCSVFile = 'enriched.csv';
    await fs.appendFile(outputCSVFile, 'App ID,developerEmail,developerWebsite,developer\n', 'utf-8');

    for (const appRow of appRows) {
      const appId = appRow['App ID'];
      const details = await gplay.app({ appId });
      const { developerEmail, developerWebsite, developer } = details;

      const enrichedRow = `${appId},${developerEmail},${developerWebsite},${developer}`;

      await fs.appendFile(outputCSVFile, enrichedRow + '\n', 'utf-8');
    }

    console.log('Enrichissement terminé !');
  } catch (error) {
    console.error('Une erreur s\'est produite :', error);
  }
})();
