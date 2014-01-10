# Filegen

Have you ever felt the need to generate files based on environment variables or
yaml files? If your answer is yes, then `filegen` can be quite helpful for
you. If your answer is no, than sorry Ma'am, this gem is not for you.

## Installation

Add this line to your application's Gemfile:

    gem 'filegen'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install filegen

This gem ships with an executable called `filegen`. It makes the power of ERB
available on the commandline.

## Usage

### General advice

Please make sure you have an ERB-template available. It needs to end with
`.erb`! Place in anywhere you like. It's important that the name of variable in
the template matches the name of environment variable or yaml-key. The lookup
is case-sensitive. If you want to get access to the variable, you need to use
the `lookup`-method.

```
lookup(<variable>)
```

The default order of lookup is: 1st environment variable and 2nd yaml file. If you want
to write the output to a file you need to redirect stdout with `>`. Otherwise
it will output the content on `$stdout`.

The order can be changed by using:
```
--order env,yaml
--order yaml,env
```

A short cut for `--order` is `-o`.

### Generate a file based on Environment Variables

The content of `template.erb`:

```erb
Hello my name is: <%= lookup('NAME') %>
```

After that you can use it with filegen.

```bash
NAME=Karl filegen template.erb > file
```

And get the following result.

```
Hello my name is: Karl
```

### Generate a file based on YAML file

The content of `template.erb`:

```erb
Hello my name is: <%= lookup('NAME') %>
```

Additionally you need to create a `YAML`-file - e.g. `names.yaml`.

```yaml
---
NAME: Karl
```

After that you can use it with filegen.

```bash
#short format
filegen -y names.yaml template.erb > file

#long format
filegen --yaml_file names.yaml template.erb > file
```

And get the following result. 

```
Hello my name is: Karl
```

## Future

* Provide an option to set the order of lookup

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
