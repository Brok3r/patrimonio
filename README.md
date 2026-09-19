# Net Worth Manager

Simple web dashboard for tracking and reviewing personal net worth. It allows you to manage assets and liabilities, view historical progress, and store backups locally or in a GitHub Gist.

![Dashboard example](docs/app_1.png)

## Features

- Track assets and liabilities with a name, category, and value.
- Automatically calculate total assets, liabilities, and net worth.
- View a monthly net worth history chart.
- View asset distribution by category.
- Edit and delete records.
- Store data locally using `localStorage`.
- Export and import JSON backups.
- Optionally synchronize data with a public or secret GitHub Gist.
- Responsive interface for desktop and mobile.

## Technologies

- HTML, CSS, and vanilla JavaScript.
- Tailwind CSS loaded through a CDN.
- Chart.js loaded through a CDN.
- GitHub Gists API for optional synchronization.

There is no custom server or database. The application can run as a static web page.

## Local Usage

Open `index.html` in your browser. The application needs an Internet connection to load Tailwind CSS, Font Awesome, Chart.js, and the external fonts.

Data is saved automatically in the browser's local storage. Therefore, clearing browser data or switching devices will make the local data unavailable. Use **Export** to create a backup.

## Backups

### Export

Click **Export** to download a file containing all current assets, liabilities, and history entries. The file is generated as JSON and can be stored in a secure location.

### Import

Click **Import** and select a previously exported JSON file. The content must have this minimum structure:

```json
{
  "items": [],
  "history": []
}
```

Importing a file replaces the data currently loaded in the application.

## GitHub Gist Synchronization

Synchronization is optional. Once configured, the application reads and updates the `patrimonio.json` file inside the Gist.

### Create a Gist from scratch

1. Sign in to [GitHub](https://github.com/).
2. Open [Create a new Gist](https://gist.github.com/).
3. Enter exactly `patrimonio.json` as the filename.
4. Enter valid initial JSON, for example:

   ```json
   {
     "items": [],
     "history": []
   }
   ```

5. Choose **Create secret gist** so the Gist does not appear in public searches.
6. Click **Create secret gist**.
7. Copy the Gist ID. It is the last part of its URL:

   ```text
   https://gist.github.com/usuario/0123456789abcdef
   																		^^^^^^^^^^^^^^^^
                                      Gist ID
   ```

### Create a GitHub token

The application needs a personal access token to read and modify the Gist.

1. In GitHub, open **Settings**.
2. Go to **Developer settings**.
3. Open **Personal access tokens**.
4. You can create a classic token with the `gist` scope, or a fine-grained token with read and write access to Gists.
5. Set a reasonable expiration date and generate the token.
6. Copy the token immediately. GitHub will not show the full token again.

Do not share the token or store it in the repository.

### Configure the application

1. In the dashboard, click the synchronization settings button with the cloud icon.
2. Enter the **Gist ID**.
3. Enter the **GitHub Token**.
4. Click **Test connection**.
5. If the test succeeds, click **Save**.

After saving, the application downloads the data from the Gist. Later changes are saved locally and sent to the Gist when a connection is available.

### Security and limitations

- The token is stored unencrypted in `localStorage` on the current device.
- Do not use this application on a shared computer if you configure a personal token.
- Revoke the token from GitHub if the device is lost or the token is exposed.
- A secret Gist is not encryption: anyone with its URL and sufficient authorization could access it.
- Synchronization does not replace exported backups.

## Disconnect synchronization

Open the synchronization settings and click **Disconnect**. This removes the credentials stored in the browser, but does not delete the Gist or local data.

## Reset the data

The trash button deletes the current data from local storage and restores the sample data included in the application.

## TODO

[] ...
