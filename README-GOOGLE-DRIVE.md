# Chisa ALT Teaching Hub v5 — Google Drive setup

This version keeps the website on GitHub Pages but stores your teaching files in **your own Google Drive**. The site creates a private folder called `Chisa ALT Teaching Hub` and uploads your PowerPoints/PDFs/Word files there.

## What v5 does

- Connects to Google Drive with Google OAuth.
- Uploads `.ppt`, `.pptx`, `.pdf`, `.doc`, and `.docx` files to your Drive.
- Keeps the original file in Drive permanently.
- Shows the files in the website from any computer after connecting the same Google account.
- **Open** opens the Drive file.
- **Download** downloads the original file.
- **Favorite** is saved as Drive file metadata.
- **Trash** moves the file to Google Drive Trash.
- Stores the category with the Drive file instead of only in browser localStorage.

## One-time Google setup

Google requires a browser OAuth Client ID before a public website can request Drive access.

1. Open Google Cloud Console and create/select a project.
2. Enable **Google Drive API**.
3. Configure **Google Auth Platform / OAuth consent** for the project.
4. Create an **OAuth 2.0 Client ID** with application type **Web application**.
5. Under **Authorized JavaScript origins**, add the exact origin of your website, for example:
   - `https://xavieraponteus-source.github.io`
   - `https://www.xavierteaching.com` if that is the final custom-domain URL you use
6. Copy the OAuth Client ID. It looks similar to:
   `1234567890-abc123.apps.googleusercontent.com`
7. Open the Chisa Hub, click **Connect Drive**, paste the Client ID, and choose **Continue with Google**.
8. Approve Drive access when Google asks.

**Do not put a Google Client Secret into the website. Web browser OAuth clients do not need a client secret.**

## Important privacy note

The app uses the `drive.file` scope. The intention is to let the app work with files it creates through the hub rather than giving the website unrestricted access to your entire Drive. Your actual teaching files remain in your Google Drive account.

If you publish the website publicly, other people can see the website itself, but they cannot automatically see your private Drive files just because they can visit the website. Google still requires the user to authorize Drive access.

## GitHub Pages

After you finish the Google Cloud setup, upload the contents of this ZIP to the same GitHub Pages repository you used for v4. The main file is `index.html` and the `assets` folder must stay beside it.

## If Google says the origin is not authorized

Make sure the Authorized JavaScript origin is the **origin only**, with no page path. For example:

`https://xavieraponteus-source.github.io`

not:

`https://xavieraponteus-source.github.io/chisa-alt-teaching-hub/`

If you use a custom domain, add the custom-domain origin too.

## Technical note

The website uses Google Identity Services in the browser and the Google Drive REST API. Access tokens are held only in the active browser session; the website does not store a Google password or client secret.
