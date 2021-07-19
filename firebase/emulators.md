# Loading data into firestore emulator

Add data in the real firestore and then export it using:
```bash
gcloud firestore export gs://{{project-id}}.appspot.com/firestore
```
The 'firestore' part in the path is just a name. This creates a backup of the
firestore database in the specified bucket.

Once that is done, download it:
```bash
gsutil -m cp -r gs://{{project-id}}.appspot.com/firestore ./emulators/
```

The last argument is the location where the previous backup will be downloaded
to. With this, we can now start the emulators and tell them to use the data
from the backup, as well as to export any changes we made:
```bash
npm run build && firebase emulators:start --only auth,functions,firestore,storage --import ./emulators --export-on-exit
```
Exporting changes will make our emulator tests kind of persistent. Any changes
we make will be commited to the data the emulators will use to initialise
firestore.

# Example (partial) package.json
```json
{
  "config": {
    "backup_path": "gs://{{project-id}}.appspot.com/firestore"
  },
  "scripts": {
    "build": "tsc",
    "serve": "npm run build && firebase emulators:start --only auth,functions,firestore,storage --import ./emulators --export-on-exit",
    "rm-local-backup": "rm -rf emulators/*",
    "create-backup": "gcloud firestore export $npm_package_config_backup_path",
    "download-backup": "gsutil -m cp -r $npm_package_config_backup_path ./emulators/",
    "rm-cloud-backup": "gsutil rm -r $npm_package_config_backup_path",
    "update-local-backup": "npm run rm-local-backup && npm run create-backup && npm run download-backup && npm run rm-cloud-backup"
  }
}
```
