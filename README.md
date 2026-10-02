# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-01T20:44:52Z
- **Commit:** [`ba050b0`](https://github.com/Hawthorne001/client_java/commit/ba050b022f6e06203df318a7871b744cc4d6a167)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 550.68M | ± 1474.27K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.59M | ± 442.12K | ops/s |
| prometheusLabelValuesInc | 115.57M | ± 2137.60K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.16M | ± 883.44K | ops/s |
| prometheusInc | 65.58K | ± 1.64K | ops/s |
| prometheusNoLabelsInc | 56.24K | ± 1.13K | ops/s |
| prometheusAdd | 51.58K | ± 68.94 | ops/s |
| codahaleIncNoLabels | 50.05K | ± 1.39K | ops/s |
| openTelemetryBoundInc | 36.25K | ± 2.48K | ops/s |
| openTelemetryBoundAdd | 31.87K | ± 273.21 | ops/s |
| openTelemetryIncNoLabels | 21.81K | ± 53.88 | ops/s |
| openTelemetryInc | 17.30K | ± 712.87 | ops/s |
| openTelemetryAdd | 15.44K | ± 233.65 | ops/s |
| simpleclientInc | 6.61K | ± 40.75 | ops/s |
| simpleclientAdd | 6.33K | ± 178.53 | ops/s |
| simpleclientNoLabelsInc | 6.27K | ± 91.03 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.07K | ± 22.84 | ops/s |
| prometheusClassic | 6.11K | ± 1.50K | ops/s |
| openTelemetryBoundClassic | 5.85K | ± 692.73 | ops/s |
| prometheusClassicSingleThread | 4.54K | ± 17.81 | ops/s |
| simpleclient | 4.41K | ± 88.25 | ops/s |
| openTelemetryClassic | 3.80K | ± 274.41 | ops/s |
| prometheusNative | 2.74K | ± 301.14 | ops/s |
| openTelemetryBoundExponential | 1.08K | ± 133.41 | ops/s |
| openTelemetryExponential | 866.53 | ± 27.22 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 23.64K | ± 664.95 | ops/s |
| prometheusWriteToNull | 23.26K | ± 492.25 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 542.26K | ± 8.16K | ops/s |
| prometheusWriteToByteArray | 539.96K | ± 7.13K | ops/s |
| openMetricsWriteToByteArray | 511.18K | ± 3.78K | ops/s |
| openMetricsWriteToNull | 509.08K | ± 3.14K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.060 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.029 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.026 | — | — |
| CounterBenchmark.openTelemetryInc | 0.054 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.043 | — | — |
| CounterBenchmark.prometheusAdd | 0.071 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.065 | — | — |
| CounterBenchmark.simpleclientAdd | 0.147 | — | — |
| CounterBenchmark.simpleclientInc | 0.140 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.148 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.161 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.869 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.245 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.071 | — | — |
| HistogramBenchmark.prometheusClassic | 0.638 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.652 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.642 | — | — |
| HistogramBenchmark.prometheusNative | 417713.364 | — | — |
| HistogramBenchmark.simpleclient | 0.211 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.148 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.150 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18448.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18448.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50048.362   ± 1388.241  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15444.247    ± 233.654  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31873.570    ± 273.208  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      36249.981   ± 2482.896  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17299.705    ± 712.874  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21807.183     ± 53.882  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51581.547     ± 68.945  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  550682267.970 ± 1474273.781  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334593020.438 ± 442121.665  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65578.931   ± 1637.486  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  115565653.501 ± 2137598.578  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58156631.856 ± 883437.305  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56236.973   ± 1133.210  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6328.222    ± 178.532  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6609.911     ± 40.753  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6272.915     ± 91.028  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5848.488    ± 692.726  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1081.190    ± 133.412  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       3796.875    ± 274.414  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        866.528     ± 27.224  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6111.921   ± 1498.691  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12073.329     ± 22.837  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4535.800     ± 17.808  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2735.157    ± 301.137  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4409.244     ± 88.250  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23642.246    ± 664.954  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23256.566    ± 492.250  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     511176.366   ± 3781.180  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     509081.677   ± 3136.630  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     539956.277   ± 7128.338  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     542264.836   ± 8156.928  ops/s
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
