# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-26T21:31:48Z
- **Commit:** [`cce26b8`](https://github.com/Hawthorne001/client_java/commit/cce26b87ccc0d8dbb83e8532ce7adba8f26c5372)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 556.92M | ± 4062.82K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.90M | ± 493.30K | ops/s |
| prometheusLabelValuesInc | 116.76M | ± 1047.47K | ops/s |
| prometheusLabelValuesIncSingleThread | 56.90M | ± 2358.86K | ops/s |
| prometheusInc | 65.97K | ± 328.12 | ops/s |
| prometheusNoLabelsInc | 57.08K | ± 117.18 | ops/s |
| prometheusAdd | 51.03K | ± 379.45 | ops/s |
| codahaleIncNoLabels | 48.42K | ± 1.39K | ops/s |
| openTelemetryBoundInc | 38.03K | ± 364.03 | ops/s |
| openTelemetryBoundAdd | 32.13K | ± 373.88 | ops/s |
| openTelemetryIncNoLabels | 23.40K | ± 1.20K | ops/s |
| openTelemetryInc | 18.23K | ± 131.07 | ops/s |
| openTelemetryAdd | 15.50K | ± 74.55 | ops/s |
| simpleclientInc | 6.54K | ± 42.66 | ops/s |
| simpleclientNoLabelsInc | 6.36K | ± 38.95 | ops/s |
| simpleclientAdd | 6.21K | ± 253.42 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 11.91K | ± 125.50 | ops/s |
| prometheusClassic | 5.99K | ± 1.69K | ops/s |
| openTelemetryBoundClassic | 5.07K | ± 1.29K | ops/s |
| openTelemetryClassic | 5.02K | ± 1.33K | ops/s |
| prometheusClassicSingleThread | 4.54K | ± 10.73 | ops/s |
| simpleclient | 4.33K | ± 110.22 | ops/s |
| prometheusNative | 2.93K | ± 282.58 | ops/s |
| openTelemetryBoundExponential | 1.02K | ± 78.07 | ops/s |
| openTelemetryExponential | 907.67 | ± 64.35 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.80K | ± 564.42 | ops/s |
| openMetricsWriteToNull | 23.49K | ± 382.88 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 546.41K | ± 11.98K | ops/s |
| prometheusWriteToByteArray | 544.78K | ± 7.22K | ops/s |
| openMetricsWriteToNull | 516.53K | ± 10.30K | ops/s |
| openMetricsWriteToByteArray | 511.52K | ± 4.01K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.060 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.029 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.024 | — | — |
| CounterBenchmark.openTelemetryInc | 0.051 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.040 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.064 | — | — |
| CounterBenchmark.simpleclientAdd | 0.149 | — | — |
| CounterBenchmark.simpleclientInc | 0.141 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.146 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.191 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.919 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.198 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.027 | — | — |
| HistogramBenchmark.prometheusClassic | 0.659 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.686 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.641 | — | — |
| HistogramBenchmark.prometheusNative | 417686.469 | — | — |
| HistogramBenchmark.simpleclient | 0.216 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.149 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.147 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18448.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18448.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48418.697   ± 1390.428  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15499.608     ± 74.549  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      32130.063    ± 373.879  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      38034.140    ± 364.026  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      18230.083    ± 131.065  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      23397.235   ± 1197.283  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51030.882    ± 379.447  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  556915690.793 ± 4062820.321  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334903630.009 ± 493297.758  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65970.418    ± 328.119  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  116761976.583 ± 1047468.770  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   56895401.765 ± 2358864.750  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57076.087    ± 117.185  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6210.224    ± 253.423  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6536.079     ± 42.664  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6355.233     ± 38.948  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5074.262   ± 1287.959  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1015.398     ± 78.069  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       5019.521   ± 1329.948  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        907.672     ± 64.352  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5994.591   ± 1689.788  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      11911.481    ± 125.500  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4544.237     ± 10.729  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2926.202    ± 282.581  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4327.120    ± 110.221  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23485.892    ± 382.878  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23798.029    ± 564.420  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     511520.163   ± 4008.759  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     516529.912  ± 10303.831  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     544781.270   ± 7216.398  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     546407.994  ± 11981.651  ops/s
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
