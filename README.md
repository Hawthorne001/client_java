# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-02T23:55:39Z
- **Commit:** [`ba050b0`](https://github.com/Hawthorne001/client_java/commit/ba050b022f6e06203df318a7871b744cc4d6a167)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 560.08M | ± 14391.60K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.78M | ± 371.21K | ops/s |
| prometheusLabelValuesInc | 116.17M | ± 1829.17K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.46M | ± 173.05K | ops/s |
| prometheusInc | 66.02K | ± 376.87 | ops/s |
| prometheusNoLabelsInc | 55.81K | ± 1.05K | ops/s |
| codahaleIncNoLabels | 49.76K | ± 483.56 | ops/s |
| prometheusAdd | 43.88K | ± 11.38K | ops/s |
| openTelemetryBoundInc | 36.65K | ± 2.48K | ops/s |
| openTelemetryBoundAdd | 31.66K | ± 142.52 | ops/s |
| openTelemetryIncNoLabels | 23.40K | ± 1.25K | ops/s |
| openTelemetryInc | 18.13K | ± 74.34 | ops/s |
| openTelemetryAdd | 15.53K | ± 176.07 | ops/s |
| simpleclientInc | 6.60K | ± 100.54 | ops/s |
| simpleclientNoLabelsInc | 6.45K | ± 185.81 | ops/s |
| simpleclientAdd | 6.31K | ± 212.52 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.07K | ± 54.97 | ops/s |
| openTelemetryBoundClassic | 7.40K | ± 1.59K | ops/s |
| prometheusClassic | 6.16K | ± 2.30K | ops/s |
| prometheusClassicSingleThread | 4.54K | ± 14.97 | ops/s |
| simpleclient | 4.37K | ± 59.93 | ops/s |
| openTelemetryClassic | 4.01K | ± 399.64 | ops/s |
| prometheusNative | 2.52K | ± 104.85 | ops/s |
| openTelemetryBoundExponential | 1.03K | ± 92.25 | ops/s |
| openTelemetryExponential | 888.64 | ± 30.92 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 24.00K | ± 663.94 | ops/s |
| openMetricsWriteToNull | 23.80K | ± 261.33 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 556.53K | ± 10.51K | ops/s |
| prometheusWriteToByteArray | 541.49K | ± 10.80K | ops/s |
| openMetricsWriteToNull | 518.10K | ± 6.90K | ops/s |
| openMetricsWriteToByteArray | 509.21K | ± 5.10K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.060 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.029 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.026 | — | — |
| CounterBenchmark.openTelemetryInc | 0.051 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.040 | — | — |
| CounterBenchmark.prometheusAdd | 0.090 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.066 | — | — |
| CounterBenchmark.simpleclientAdd | 0.148 | — | — |
| CounterBenchmark.simpleclientInc | 0.141 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.144 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.133 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.902 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.234 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.046 | — | — |
| HistogramBenchmark.prometheusClassic | 0.675 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.665 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.642 | — | — |
| HistogramBenchmark.prometheusNative | 417677.136 | — | — |
| HistogramBenchmark.simpleclient | 0.213 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.147 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.146 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18448.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18429.335 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49761.174    ± 483.559  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15527.348    ± 176.066  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31655.170    ± 142.517  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      36649.741   ± 2484.339  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      18128.014     ± 74.339  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      23395.267   ± 1246.632  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      43878.211  ± 11380.269  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  560077155.442 ± 14391604.518  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334784203.723 ± 371210.488  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66020.875    ± 376.871  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  116171780.027 ± 1829165.054  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58464131.142 ± 173048.133  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55813.759   ± 1049.664  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6312.873    ± 212.524  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6597.009    ± 100.537  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6448.415    ± 185.813  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       7404.714   ± 1585.698  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1034.095     ± 92.250  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4006.536    ± 399.645  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        888.640     ± 30.917  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6157.519   ± 2299.056  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12069.884     ± 54.972  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4535.831     ± 14.975  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2522.668    ± 104.846  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4367.440     ± 59.933  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23798.873    ± 261.325  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23999.181    ± 663.945  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509207.952   ± 5098.773  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     518099.237   ± 6899.496  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     541491.619  ± 10804.411  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556527.334  ± 10514.314  ops/s
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
