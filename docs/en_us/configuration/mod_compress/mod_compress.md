# Introductionn

mod_compress compresses responses using specified method.

# Module configuration
## Description
conf/mod_compress/mod_compress.conf

| Config Item          | Description                                 |
| ---------------------| ------------------------------------------- |
| Basic.DataPath       | String<br>Path of rule configuration |
| Log.OpenDebug        | Boolean<br>Whether enable debug logs<br>Default False |

## Example
```
[basic]
DataPath = ../conf/mod_compress/compress_rule.data

[log]
OpenDebug = false
```

# Rule configuration
## Description
| Config Item | Description                                                |
| ----------- | -------------------------------------------------------------- |
| Version | String<br>Vesion of config file |
| Config | Object<br>Compress rule for each product |
| Config{k} | String<br>Product name |
| Config{v} | Object<br>A list of compress rules |
| Config{v}[] | Object<br>A compress rule |
| Config{v}[].Cond | String<br>Condition expression, See [Condition](../../condition/condition_grammar.md) |
| Config{v}[].Action | Object<br>Action |
| Config{v}[].Action.Cmd | String<br>Name of Action |
| Config{v}[].Action.Quality | Integer<br>Compression level |
| Config{v}[].Action.FlushSize | Integer<br>Flush size |

## Module Actions

| Action                  | Descrition                          |
| ------------------------| ------------------------------------|
| GZIP                    | Compress response using gzip method |

## Example
```
{
    "Config": {
        "example_product": [
            {
                "Cond": "req_host_in(\"www.example.org\")",
                "Action": {
                    "Cmd": "GZIP",
                    "Quality": 9,
                    "FlushSize": 512
                }
            }
        ]
    },
    "Version": "20190101000000"
}
```