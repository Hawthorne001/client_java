# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-06T10:44:03Z
- **Commit:** [`ba050b0`](https://github.com/Hawthorne001/client_java/commit/ba050b022f6e06203df318a7871b744cc4d6a167)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 547.13M | ± 16204.29K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.49M | ± 596.81K | ops/s |
| prometheusLabelValuesInc | 117.06M | ± 2070.38K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.52M | ± 183.87K | ops/s |
| prometheusInc | 65.49K | ± 1.41K | ops/s |
| prometheusNoLabelsInc | 56.15K | ± 938.21 | ops/s |
| prometheusAdd | 50.35K | ± 1.36K | ops/s |
| codahaleIncNoLabels | 48.18K | ± 1.17K | ops/s |
| openTelemetryBoundInc | 38.19K | ± 232.44 | ops/s |
| openTelemetryBoundAdd | 31.48K | ± 290.49 | ops/s |
| openTelemetryIncNoLabels | 21.97K | ± 109.43 | ops/s |
| openTelemetryInc | 18.20K | ± 108.31 | ops/s |
| openTelemetryAdd | 15.55K | ± 77.97 | ops/s |
| simpleclientInc | 6.59K | ± 11.05 | ops/s |
| simpleclientNoLabelsInc | 6.32K | ± 31.83 | ops/s |
| simpleclientAdd | 6.30K | ± 168.88 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.12K | ± 48.29 | ops/s |
| prometheusClassic | 6.84K | ± 2.18K | ops/s |
| openTelemetryBoundClassic | 6.02K | ± 1.96K | ops/s |
| prometheusClassicSingleThread | 4.44K | ± 134.78 | ops/s |
| openTelemetryClassic | 4.39K | ± 900.49 | ops/s |
| simpleclient | 4.38K | ± 19.20 | ops/s |
| prometheusNative | 2.90K | ± 244.68 | ops/s |
| openTelemetryBoundExponential | 1.09K | ± 20.90 | ops/s |
| openTelemetryExponential | 790.50 | ± 79.07 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 23.58K | ± 831.77 | ops/s |
| openMetricsWriteToNull | 23.44K | ± 439.46 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 539.94K | ± 16.52K | ops/s |
| prometheusWriteToByteArray | 529.62K | ± 6.42K | ops/s |
| openMetricsWriteToNull | 513.89K | ± 7.65K | ops/s |
| openMetricsWriteToByteArray | 509.82K | ± 4.97K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.060 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.030 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.024 | — | — |
| CounterBenchmark.openTelemetryInc | 0.051 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.042 | — | — |
| CounterBenchmark.prometheusAdd | 0.073 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.056 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.065 | — | — |
| CounterBenchmark.simpleclientAdd | 0.147 | — | — |
| CounterBenchmark.simpleclientInc | 0.141 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.146 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.167 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.851 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.221 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.182 | — | — |
| HistogramBenchmark.prometheusClassic | 0.584 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.666 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.656 | — | — |
| HistogramBenchmark.prometheusNative | 417713.290 | — | — |
| HistogramBenchmark.simpleclient | 0.213 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.149 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.149 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18429.335 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18448.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48176.066   ± 1169.924  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15551.728     ± 77.967  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31477.865    ± 290.495  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      38192.800    ± 232.441  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      18198.881    ± 108.310  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      21967.756    ± 109.431  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50347.580   ± 1358.576  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  547132344.540 ± 16204285.912  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334486261.061 ± 596807.990  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65494.764   ± 1408.236  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  117055027.883 ± 2070376.183  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58519047.790 ± 183872.769  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56148.515    ± 938.213  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6300.229    ± 168.878  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6586.337     ± 11.055  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6316.379     ± 31.826  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6024.049   ± 1962.940  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1090.706     ± 20.903  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4390.781    ± 900.494  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        790.504     ± 79.069  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6842.603   ± 2180.867  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12124.058     ± 48.287  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4441.023    ± 134.778  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2895.731    ± 244.679  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4383.363     ± 19.205  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23435.565    ± 439.457  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23582.322    ± 831.767  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509819.888   ± 4968.175  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     513887.186   ± 7647.235  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     529623.648   ± 6415.044  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     539944.416  ± 16519.822  ops/s
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
