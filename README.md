jcli
====

Janrain CLI.

## Install from source

```
git clone git@github.com:xwp/janrain-cli-tools.git jcli
cd jcli
composer install
```

Done. You can run via `./bin/jcli` from current directory.

If you want to build the phar file:

```
box build
```

and you can move the file to your OS `PATH`:

```
mv jcli.phar /usr/local/bin/jcli
```

Now you can run `jcli` from anywhere.

## Configure

The first time you need to do is configure your `jcli`. By default `client_id`,
`client_secret`, and `base_url` are empty:

```
jcli config -l
```

These are required config keys that need to be set. Set it with:

```
jcli config client_id YOUR_CLIENT_ID
jcli config client_secret YOUR_CLIENT_SECRET
jcli config base_url YOUR_BASE_URL
```

Additionaly you can set `default_type` to set default entity type. Now, everytime
you run command you can ignore `-t` option.

```
jcli config default_type user
```

## Commands

```
$ ./bin/jcli
jcli version @package_version@

Usage:
  command [options] [arguments]

Options:
  -h, --help            Display this help message
  -q, --quiet           Do not output any message
  -V, --version         Display this application version
      --ansi            Force ANSI output
      --no-ansi         Disable ANSI output
  -n, --no-interaction  Do not ask any interactive question
  -v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

Available commands:
  config                 Janrain config
  help                   Displays help for a command
  list                   Lists commands
 entity
  entity:count           Retrieve number of records of entity type
  entity:fill-unsub-key  Fill empty unsubscribe key on records
  entity:find            Find entity
  entity:update          Update an entity
  entity:view            Retrieve a single entity
 type
  type:list              Retrieve all entity types
```

### Find records

```
jcli entity:find "gender != 'male'"
```

Limit the output to 10 records:

```
jcli entity:find "gender != 'male'" -m 10
```

Specifying offset (start from 5th record):

```
jcli entity:find "gender != 'male'" -m 10 -f 5
```

### Count records

```
jcli entity:count "gender != 'male' AND birthday is not null"
```

### View a single record

```
jcli entity:view id=999
jcli entity:view uuid=c0613105-f632-41ce-80eb-56668df7fc83
```

### Update a record

```
jcli entity:update id=999 givenName=Akeda displayName="Akeda Bagus"
```

### Update all empty ETUID attributes

```
jcli entity:fill-unsub-key
```
You may get API rate limit from Janrain. If so, the jcli will output the
message. When that happens, you can re-run `jcli
entity:fill-unsub-key` again for the remaining records.