# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-08T10:34:46Z
- **Commit:** [`ba050b0`](https://github.com/Hawthorne001/client_java/commit/ba050b022f6e06203df318a7871b744cc4d6a167)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 737.99M | ± 9264.91K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 219.40M | ± 2771.53K | ops/s |
| prometheusLabelValuesInc | 208.62M | ± 5675.45K | ops/s |
| prometheusLabelValuesIncSingleThread | 96.56M | ± 1770.88K | ops/s |
| prometheusInc | 65.72K | ± 3.53K | ops/s |
| prometheusNoLabelsInc | 63.94K | ± 1.93K | ops/s |
| codahaleIncNoLabels | 63.84K | ± 2.96K | ops/s |
| prometheusAdd | 58.31K | ± 2.26K | ops/s |
| openTelemetryBoundInc | 52.18K | ± 1.31K | ops/s |
| openTelemetryBoundAdd | 48.07K | ± 498.58 | ops/s |
| openTelemetryIncNoLabels | 34.11K | ± 1.18K | ops/s |
| openTelemetryInc | 29.48K | ± 1.80K | ops/s |
| openTelemetryAdd | 25.10K | ± 1.54K | ops/s |
| simpleclientNoLabelsInc | 11.09K | ± 135.14 | ops/s |
| simpleclientInc | 10.89K | ± 139.03 | ops/s |
| simpleclientAdd | 10.16K | ± 182.45 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 14.42K | ± 178.41 | ops/s |
| prometheusClassic | 10.60K | ± 1.55K | ops/s |
| openTelemetryBoundClassic | 9.41K | ± 498.85 | ops/s |
| simpleclient | 6.65K | ± 103.51 | ops/s |
| openTelemetryClassic | 4.77K | ± 71.64 | ops/s |
| prometheusNative | 4.51K | ± 359.21 | ops/s |
| prometheusClassicSingleThread | 4.32K | ± 31.31 | ops/s |
| openTelemetryBoundExponential | 1.12K | ± 17.99 | ops/s |
| openTelemetryExponential | 998.66 | ± 21.00 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 31.45K | ± 360.01 | ops/s |
| openMetricsWriteToNull | 31.27K | ± 599.98 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 856.38K | ± 14.46K | ops/s |
| prometheusWriteToNull | 826.18K | ± 52.25K | ops/s |
| openMetricsWriteToNull | 701.22K | ± 12.71K | ops/s |
| openMetricsWriteToByteArray | 684.47K | ± 10.49K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.015 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.038 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.020 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.018 | — | — |
| CounterBenchmark.openTelemetryInc | 0.032 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.027 | — | — |
| CounterBenchmark.prometheusAdd | 0.063 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.057 | — | — |
| CounterBenchmark.simpleclientAdd | 0.092 | — | — |
| CounterBenchmark.simpleclientInc | 0.087 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.085 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.100 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.843 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.197 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.941 | — | — |
| HistogramBenchmark.prometheusClassic | 0.353 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.555 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.653 | — | — |
| HistogramBenchmark.prometheusNative | 417712.852 | — | — |
| HistogramBenchmark.simpleclient | 0.141 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.112 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.111 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18448.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18429.334 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      63841.168   ± 2956.038  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      25101.672   ± 1535.009  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      48068.952    ± 498.581  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      52177.036   ± 1309.252  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      29478.972   ± 1804.529  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      34113.878   ± 1183.038  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      58308.735   ± 2263.831  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  737989623.647 ± 9264909.180  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  219398155.479 ± 2771532.704  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65717.493   ± 3525.849  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  208617540.666 ± 5675454.581  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   96560702.341 ± 1770877.232  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      63939.507   ± 1933.047  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10160.829    ± 182.449  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10886.046    ± 139.026  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      11094.008    ± 135.142  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       9412.371    ± 498.853  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1115.461     ± 17.993  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4770.840     ± 71.641  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        998.665     ± 20.997  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15      10599.015   ± 1547.918  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      14421.555    ± 178.410  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4323.085     ± 31.313  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4512.848    ± 359.205  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6646.066    ± 103.515  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      31271.790    ± 599.980  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      31447.241    ± 360.011  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     684470.404  ± 10490.170  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     701219.928  ± 12705.005  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     856380.329  ± 14460.958  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     826183.735  ± 52248.404  ops/s
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
