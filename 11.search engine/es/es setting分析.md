```
{
    "tungee_ads_manufacturing_customer_group_v20221205": {
        "settings": {
            "index": {
                "refresh_interval": "-1",
                "number_of_shards": "40",
                "translog": {
                    "flush_threshold_size": "1gb",
                    "sync_interval": "20s",
                    "durability": "async"
                },
                "provided_name": "tungee_ads_manufacturing_customer_group_v20221205",
                "merge": {
                    "policy": {
                        "max_merged_segment": "6gb"
                    }
                },
                "max_result_window": "200000",
                "creation_date": "1688983164691",
                "sort": {
                    "field": [
                        "tungeeRank",
                        "uuid"
                    ],
                    "order": [
                        "desc",
                        "asc"
                    ]
                },
                "analysis": {
                    "normalizer": {
                        "lowercase": {
                            "filter": [
                                "lowercase"
                            ],
                            "type": "custom"
                        }
                    },
                    "analyzer": {
                        "tg_short_text_lowercase": {
                            "filter": [
                                "lowercase"
                            ],
                            "type": "custom",
                            "tokenizer": "ngram_tokenizer"
                        },
                        "tg_short_text": {
                            "type": "custom",
                            "tokenizer": "ngram_tokenizer"
                        },
                        "pinyin_analyzer": {
                            "tokenizer": "pinyin_tokenizer"
                        }
                    },
                    "tokenizer": {
                        "pinyin_tokenizer": {
                            "ignore_pinyin_offset": "false",
                            "lowercase": "true",
                            "keep_original": "false",
                            "remove_duplicated_term": "false",
                            "keep_first_letter": "false",
                            "keep_separate_first_letter": "false",
                            "type": "pinyin",
                            "limit_first_letter_length": "16",
                            "keep_full_pinyin": "true"
                        },
                        "ngram_tokenizer": {
                            "token_chars": [
                                "letter",
                                "digit",
                                "punctuation"
                            ],
                            "min_gram": "1",
                            "type": "ngram",
                            "max_gram": "1"
                        }
                    }
                },
                "number_of_replicas": "0",
                "uuid": "Pc33mrNhRuWKN_PPupq3rg",
                "version": {
                    "created": "7040299"
                }
            }
        }
    }
}
```

- 这个Elasticsearch索引的设置配置包含了一系列参数和属性，用于定义索引的行为和性能。让我为您解释这些设置的含义：

  1. `"refresh_interval": "-1"`：这表示关闭了自动刷新，因为刷新间隔被设置为负数 `-1`。这意味着新文档不会自动刷新到磁盘，需要手动触发刷新操作才能使新数据对搜索可见。

  2. `"number_of_shards": "40"`：这指定了索引的主分片数量。索引被分成了40个主分片，用于存储索引的数据。主分片的数量在索引创建时是固定的，影响索引的数据分布和性能。

  3. `"translog"`：这部分包含有关事务日志（translog）的配置。
     - `"flush_threshold_size": "1gb"`：指定了事务日志的刷新阈值大小。当事务日志达到1GB时，将执行事务日志的刷新操作。
     - `"sync_interval": "20s"`：定义了同步事务日志的时间间隔，每隔20秒同步一次。
     - `"durability": "async"`：指定了事务日志的耐久性模式，异步模式表示不需要等待数据写入磁盘，提高写入性能。

  4. `"merge"`：这部分包含有关索引段合并（segment merge）的配置。
     - `"policy"`：定义了段合并的策略。
       - `"max_merged_segment": "6gb"`：指定了合并后的段的最大大小，当达到6GB时将执行段合并操作。

  5. `"max_result_window": "200000"`：定义了搜索请求的最大结果窗口大小。这是用来限制一次搜索请求返回的最大文档数量，以防止大量文档被一次性请求。

  6. `"analysis"`：这包含了分析器（analyzer）和标准化器（normalizer）的定义，用于文本分析和索引。
     - `"normalizer"`：定义了一个名为 "lowercase" 的标准化器，它会将所有文本转换为小写。
     - `"analyzer"`：定义了多个自定义分析器，包括 "tg_short_text_lowercase"、"tg_short_text" 和 "pinyin_analyzer"，每个分析器使用不同的分词器（tokenizer）和过滤器（filter）。

  7. `"tokenizer"`：定义了两种分词器，其中包括 "pinyin_tokenizer" 和 "ngram_tokenizer"，用于中文拼音处理和文本分词。

  8. `"number_of_replicas": "0"`：指定了索引的副本数量。这里设置为0，表示没有副本，只有主分片，意味着数据不会被复制到其他节点上。

  9. `"uuid": "Pc33mrNhRuWKN_PPupq3rg"`：表示索引的唯一标识符，每个索引都有一个唯一的UUID。

  10. `"version"`：包含了索引的版本信息，包括索引的创建版本。

  这些设置配置影响了索引的性能、实时性和存储行为。例如，关闭自动刷新会降低实时性，但可以提高写入性能。主分片数量、副本数量和分析器配置也会影响索引的性能和行为。对于每个具体的应用场景，需要根据需求和硬件资源来合理配置这些参数以达到最佳性能。

## translog

- Elasticsearch的"translog"（事务日志）是一种核心组件，用于确保数据的持久性和可恢复性。事务日志记录了在索引中进行的所有更改操作，以便在发生故障或崩溃时能够重新构建数据。

  以下是有关Elasticsearch事务日志（translog）的一些关键信息：

  1. **事务日志的作用**：
     - 持久性：事务日志确保了写入操作的持久性，即使Elasticsearch节点崩溃或关闭，写入操作的数据也不会丢失。
     - 快速恢复：事务日志允许Elasticsearch在启动时快速恢复未提交的操作，以恢复到上一个稳定状态。

  2. **事务日志的类型**：
     - 事务日志有两种类型：预写日志（write-ahead log，WAL）和转发日志（forward log）。
     - 预写日志（WAL）用于记录写入操作，确保数据持久性。
     - 转发日志（forward log）用于记录读操作，以便其他节点能够跟踪读操作。

  3. **事务日志的刷新和同步**：
     - 事务日志的刷新是将缓冲区中的写入操作写入磁盘的过程，以确保数据持久性。默认情况下，Elasticsearch每隔一段时间会执行一次刷新操作。
     - 事务日志的同步是等待写入操作成功写入磁盘后才认为操作已提交的过程。同步操作确保了数据的可恢复性。

  4. **事务日志的清理**：
     - 事务日志不会一直增长，Elasticsearch会定期清理旧的事务日志。
     - 清理过程中，Elasticsearch会检查哪些日志已经被持久化到磁盘，并且不再需要保留。
     
  5. **事务日志的配置**：
     - 您可以通过配置来控制事务日志的大小、同步策略、刷新频率等参数，以根据应用需求和硬件资源进行优化。

  总之，Elasticsearch的事务日志（translog）是确保数据持久性和可恢复性的关键组件。它记录了所有写入操作，使得在发生故障或崩溃时能够恢复数据到一致的状态，同时还支持快速的数据恢复。通过适当配置事务日志参数，可以根据应用程序的需求来平衡性能和数据安全性。

## 段合并：

- 在 Elasticsearch 中，段合并（Segment Merge）是一个重要的索引维护操作，用于优化索引的性能和存储效率。段合并的主要目的是将多个小的段（segments）合并为较大的段，从而减少磁盘上的段数量，提高查询性能，并降低存储成本。

  以下是有关 Elasticsearch 中段合并操作的一些关键信息：

  1. **索引段**：
     - Elasticsearch 索引被分成多个段，每个段是一个独立的存储单元，包含一部分索引数据。
     - 当文档被添加、更新或删除时，索引中的一个或多个段会发生变化。

  2. **段合并的目的**：
     - 减少段数量：当索引中存在大量小型段时，查询性能可能受到影响，因为每次查询都需要搜索多个段。段合并操作可以将这些小段合并为较大的段。
     - 优化存储：合并段还可以提高存储效率，因为较大的段通常更紧凑，占用更少的磁盘空间。

  3. **触发段合并**：
     - Elasticsearch 自动触发段合并操作，具体触发条件包括：
       - 索引刷新时：默认情况下，索引刷新操作会触发段合并。
       - 索引合并策略：您可以配置索引的合并策略，以控制何时触发合并。
     - 手动触发：您还可以手动触发段合并操作。

  4. **段合并策略**：
     - Elasticsearch 具有不同的段合并策略，例如 "force merge" 策略，可以在需要时强制触发段合并操作。
     - 段合并策略的选择取决于您的索引和查询需求。

  5. **段合并的影响**：
     - 段合并操作可能会占用大量CPU和磁盘IO资源，因此建议在负载较低的时候执行。
     - 合并操作期间，索引可能会变得不可用，因为正在进行合并。

  6. **手动触发段合并**：
     - 您可以使用 `_forcemerge` API 手动触发段合并操作，将索引中的所有段合并为一个或少数几个大段。
     - 请注意，手动触发段合并操作需要谨慎，因为它可能会消耗大量资源。

  总之，段合并是 Elasticsearch 中的一个关键维护操作，用于优化性能和存储。自动触发的合并操作会在索引维护中运行，但您也可以根据需要手动触发合并操作。了解段合并操作可以帮助您更好地管理和优化 Elasticsearch 索引。