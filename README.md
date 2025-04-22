# Configure Payload CMS to use uuid
## Go into /src/payload.config.ts
Once you open the file, add the attribute `idType: 'uuid'` to your postgresAdapter in the buildConfig:

    db:  postgresAdapter({
	    idType:  'uuid', <-- Add it here
	    pool: {
		    connectionString:  process.env.DATABASE_URI || '',
		    },
		}),
so that your build config looks like this:

    export  default  buildConfig({
    admin: {
    user:  Users.slug,
    importMap: {
    baseDir:  path.resolve(dirname),
    },
    },
    collections: [Users, Media, Organization],
    editor:  lexicalEditor(),
    secret:  process.env.PAYLOAD_SECRET || '',
    typescript: {
    outputFile:  path.resolve(dirname, 'payload-types.ts'),
    },
    db:  postgresAdapter({
    idType:  'uuid',
    pool: {
    connectionString:  process.env.DATABASE_URI || '',
    },
    }),
    sharp,
    plugins: [
    payloadCloudPlugin(),
    // storage-adapter-placeholder
    ],
    })
## 2 Use the sql-Script in the repository.
Once done, create your postgres database and execute the `init.sql` File.

## 3 Done
Have fun using uuid!
