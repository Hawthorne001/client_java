# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-03T09:47:19Z
- **Commit:** [`ba050b0`](https://github.com/Hawthorne001/client_java/commit/ba050b022f6e06203df318a7871b744cc4d6a167)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 723.32M | ± 22387.25K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 223.23M | ± 848.11K | ops/s |
| prometheusLabelValuesInc | 212.88M | ± 4155.41K | ops/s |
| prometheusLabelValuesIncSingleThread | 99.68M | ± 550.63K | ops/s |
| prometheusInc | 70.01K | ± 301.59 | ops/s |
| prometheusNoLabelsInc | 67.83K | ± 478.26 | ops/s |
| codahaleIncNoLabels | 62.74K | ± 226.98 | ops/s |
| prometheusAdd | 58.02K | ± 133.68 | ops/s |
| openTelemetryBoundInc | 54.90K | ± 155.12 | ops/s |
| openTelemetryBoundAdd | 49.20K | ± 201.35 | ops/s |
| openTelemetryIncNoLabels | 36.88K | ± 733.58 | ops/s |
| openTelemetryInc | 30.03K | ± 960.65 | ops/s |
| openTelemetryAdd | 25.68K | ± 1.05K | ops/s |
| simpleclientNoLabelsInc | 11.36K | ± 29.54 | ops/s |
| simpleclientInc | 11.13K | ± 268.83 | ops/s |
| simpleclientAdd | 10.91K | ± 327.28 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 15.58K | ± 52.44 | ops/s |
| prometheusClassic | 9.77K | ± 391.17 | ops/s |
| openTelemetryBoundClassic | 8.13K | ± 2.16K | ops/s |
| simpleclient | 7.17K | ± 76.56 | ops/s |
| openTelemetryClassic | 6.10K | ± 1.91K | ops/s |
| prometheusNative | 5.05K | ± 116.42 | ops/s |
| prometheusClassicSingleThread | 4.55K | ± 25.38 | ops/s |
| openTelemetryBoundExponential | 1.08K | ± 60.83 | ops/s |
| openTelemetryExponential | 957.89 | ± 34.68 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 34.07K | ± 367.93 | ops/s |
| openMetricsWriteToNull | 34.06K | ± 395.66 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 875.31K | ± 15.13K | ops/s |
| prometheusWriteToByteArray | 872.07K | ± 12.89K | ops/s |
| openMetricsWriteToByteArray | 762.55K | ± 45.54K | ops/s |
| openMetricsWriteToNull | 742.36K | ± 9.99K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.015 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.037 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.019 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.017 | — | — |
| CounterBenchmark.openTelemetryInc | 0.031 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.025 | — | — |
| CounterBenchmark.prometheusAdd | 0.063 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.053 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.054 | — | — |
| CounterBenchmark.simpleclientAdd | 0.087 | — | — |
| CounterBenchmark.simpleclientInc | 0.085 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.083 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.123 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.870 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.168 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.984 | — | — |
| HistogramBenchmark.prometheusClassic | 0.378 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.518 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.609 | — | — |
| HistogramBenchmark.prometheusNative | 417712.753 | — | — |
| HistogramBenchmark.simpleclient | 0.133 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.103 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.103 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18448.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18448.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      62744.506    ± 226.976  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      25681.994   ± 1050.322  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      49203.770    ± 201.349  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      54898.189    ± 155.124  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      30025.834    ± 960.647  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      36875.122    ± 733.584  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58022.642    ± 133.683  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  723315846.224 ± 22387251.898  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  223233172.365 ± 848109.663  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      70008.101    ± 301.587  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  212875761.450 ± 4155412.062  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   99680872.097 ± 550625.958  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67827.540    ± 478.263  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10912.407    ± 327.284  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      11128.058    ± 268.835  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      11357.070     ± 29.545  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       8130.711   ± 2158.379  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1084.627     ± 60.831  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       6098.083   ± 1913.051  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        957.895     ± 34.683  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9773.105    ± 391.170  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      15583.466     ± 52.441  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4551.537     ± 25.383  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5050.098    ± 116.423  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       7174.518     ± 76.556  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      34061.416    ± 395.658  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      34074.134    ± 367.932  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     762554.285  ± 45539.474  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     742364.942   ± 9987.828  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     872065.738  ± 12891.806  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     875312.594  ± 15127.872  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter updates and label-value lookup (selected methods only) |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
