# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-05T10:39:38Z
- **Commit:** [`ba050b0`](https://github.com/Hawthorne001/client_java/commit/ba050b022f6e06203df318a7871b744cc4d6a167)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 551.13M | ± 7269.13K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.83M | ± 335.45K | ops/s |
| prometheusLabelValuesInc | 117.79M | ± 1885.04K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.70M | ± 147.35K | ops/s |
| prometheusInc | 66.48K | ± 579.58 | ops/s |
| prometheusNoLabelsInc | 56.67K | ± 256.23 | ops/s |
| prometheusAdd | 51.03K | ± 140.33 | ops/s |
| codahaleIncNoLabels | 49.43K | ± 1.28K | ops/s |
| openTelemetryBoundInc | 38.25K | ± 134.29 | ops/s |
| openTelemetryBoundAdd | 31.49K | ± 205.21 | ops/s |
| openTelemetryIncNoLabels | 22.63K | ± 1.20K | ops/s |
| openTelemetryInc | 18.08K | ± 192.41 | ops/s |
| openTelemetryAdd | 15.64K | ± 95.96 | ops/s |
| simpleclientInc | 6.54K | ± 52.36 | ops/s |
| simpleclientNoLabelsInc | 6.35K | ± 51.18 | ops/s |
| simpleclientAdd | 6.16K | ± 227.25 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.08K | ± 51.57 | ops/s |
| prometheusClassic | 5.77K | ± 1.98K | ops/s |
| openTelemetryBoundClassic | 5.76K | ± 1.27K | ops/s |
| prometheusClassicSingleThread | 4.54K | ± 12.88 | ops/s |
| simpleclient | 4.36K | ± 79.77 | ops/s |
| openTelemetryClassic | 4.35K | ± 817.57 | ops/s |
| prometheusNative | 2.96K | ± 250.21 | ops/s |
| openTelemetryBoundExponential | 1.10K | ± 31.59 | ops/s |
| openTelemetryExponential | 842.69 | ± 58.22 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.75K | ± 534.47 | ops/s |
| openMetricsWriteToNull | 23.31K | ± 812.59 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 557.31K | ± 8.59K | ops/s |
| prometheusWriteToByteArray | 542.03K | ± 23.43K | ops/s |
| openMetricsWriteToByteArray | 517.34K | ± 8.36K | ops/s |
| openMetricsWriteToNull | 517.28K | ± 8.05K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.059 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.030 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.024 | — | — |
| CounterBenchmark.openTelemetryInc | 0.051 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.041 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.055 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.065 | — | — |
| CounterBenchmark.simpleclientAdd | 0.150 | — | — |
| CounterBenchmark.simpleclientInc | 0.142 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.146 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.167 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.850 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.220 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.110 | — | — |
| HistogramBenchmark.prometheusClassic | 0.692 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.666 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.641 | — | — |
| HistogramBenchmark.prometheusNative | 417713.257 | — | — |
| HistogramBenchmark.simpleclient | 0.215 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.150 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.147 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18448.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18448.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49427.342   ± 1277.796  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15641.442     ± 95.962  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31489.344    ± 205.215  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      38252.030    ± 134.290  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      18081.387    ± 192.414  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22631.067   ± 1198.761  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51028.884    ± 140.331  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  551130866.739 ± 7269125.213  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334829252.297 ± 335449.931  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66481.947    ± 579.583  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  117793550.514 ± 1885043.782  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58695000.155 ± 147345.257  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56671.909    ± 256.232  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6159.328    ± 227.246  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6544.248     ± 52.364  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6345.296     ± 51.178  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5762.733   ± 1268.360  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1096.690     ± 31.587  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4349.736    ± 817.569  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        842.687     ± 58.221  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5773.004   ± 1980.738  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12080.779     ± 51.574  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4539.829     ± 12.876  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2961.469    ± 250.210  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4361.405     ± 79.769  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23309.100    ± 812.591  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23751.891    ± 534.470  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     517336.682   ± 8358.282  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     517280.763   ± 8046.056  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     542032.638  ± 23432.304  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     557314.212   ± 8585.469  ops/s
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
