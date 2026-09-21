# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-20T17:16:43Z
- **Commit:** [`c658f3d`](https://github.com/Hawthorne001/client_java/commit/c658f3da2d8c6f5e90837dcd3681b744242d796d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** Intel(R) Xeon(R) 6973P-C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 357.36M | ± 5740.21K | ops/s |
| prometheusLabelValuesInc | 169.66M | ± 2190.79K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 131.54M | ± 2777.15K | ops/s |
| prometheusLabelValuesIncSingleThread | 64.96M | ± 692.41K | ops/s |
| prometheusAdd | 36.17K | ± 840.77 | ops/s |
| prometheusInc | 35.06K | ± 713.43 | ops/s |
| openTelemetryBoundAdd | 35.04K | ± 768.51 | ops/s |
| openTelemetryBoundInc | 35.02K | ± 742.15 | ops/s |
| codahaleIncNoLabels | 34.76K | ± 1.44K | ops/s |
| prometheusNoLabelsInc | 33.87K | ± 1.45K | ops/s |
| openTelemetryIncNoLabels | 30.44K | ± 968.33 | ops/s |
| openTelemetryInc | 27.18K | ± 532.66 | ops/s |
| openTelemetryAdd | 23.87K | ± 645.91 | ops/s |
| simpleclientInc | 9.15K | ± 79.65 | ops/s |
| simpleclientNoLabelsInc | 8.98K | ± 117.54 | ops/s |
| simpleclientAdd | 8.89K | ± 226.90 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 9.17K | ± 221.12 | ops/s |
| simpleclient | 6.02K | ± 107.03 | ops/s |
| prometheusClassicSingleThread | 4.52K | ± 69.59 | ops/s |
| prometheusClassic | 4.17K | ± 2.56K | ops/s |
| openTelemetryClassic | 2.39K | ± 596.91 | ops/s |
| openTelemetryBoundClassic | 2.18K | ± 78.97 | ops/s |
| prometheusNative | 2.14K | ± 370.83 | ops/s |
| openTelemetryBoundExponential | 508.03 | ± 18.92 | ops/s |
| openTelemetryExponential | 464.74 | ± 16.24 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 24.96K | ± 478.27 | ops/s |
| openMetricsWriteToNull | 24.59K | ± 946.93 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 348.40K | ± 3.44K | ops/s |
| prometheusWriteToNull | 346.77K | ± 4.00K | ops/s |
| openMetricsWriteToByteArray | 330.39K | ± 5.11K | ops/s |
| openMetricsWriteToNull | 328.53K | ± 2.79K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.027 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.039 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.027 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.027 | — | — |
| CounterBenchmark.openTelemetryInc | 0.034 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.031 | — | — |
| CounterBenchmark.prometheusAdd | 0.104 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.107 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.110 | — | — |
| CounterBenchmark.simpleclientAdd | 0.105 | — | — |
| CounterBenchmark.simpleclientInc | 0.102 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.104 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.432 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 1.843 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.412 | — | — |
| HistogramBenchmark.openTelemetryExponential | 2.017 | — | — |
| HistogramBenchmark.prometheusClassic | 1.181 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.879 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.605 | — | — |
| HistogramBenchmark.prometheusNative | 335793.791 | — | — |
| HistogramBenchmark.simpleclient | 0.156 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.142 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.140 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.002 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.002 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18466.669 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18448.002 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      34760.027   ± 1437.332  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      23873.172    ± 645.905  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      35040.148    ± 768.512  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      35019.486    ± 742.149  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      27182.694    ± 532.662  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      30442.871    ± 968.333  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      36166.511    ± 840.769  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  357359444.982 ± 5740205.010  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  131543675.786 ± 2777151.135  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      35060.627    ± 713.427  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  169663449.833 ± 2190786.135  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   64956250.999 ± 692409.355  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      33873.009   ± 1449.318  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       8893.168    ± 226.897  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       9148.025     ± 79.651  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       8977.958    ± 117.543  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       2176.298     ± 78.970  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15        508.032     ± 18.921  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       2392.498    ± 596.912  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        464.741     ± 16.236  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4169.238   ± 2563.187  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15       9165.983    ± 221.117  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4516.200     ± 69.588  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2137.122    ± 370.829  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6016.953    ± 107.027  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24585.961    ± 946.933  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24955.106    ± 478.269  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     330390.185   ± 5109.557  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     328526.341   ± 2785.429  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     348401.103   ± 3443.356  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     346765.799   ± 3995.472  ops/s
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
