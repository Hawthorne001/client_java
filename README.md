# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-04T09:55:16Z
- **Commit:** [`ba050b0`](https://github.com/Hawthorne001/client_java/commit/ba050b022f6e06203df318a7871b744cc4d6a167)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 9V45 96-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 723.18M | ± 15173.00K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 216.47M | ± 2193.28K | ops/s |
| prometheusLabelValuesInc | 207.89M | ± 4059.31K | ops/s |
| prometheusLabelValuesIncSingleThread | 95.14M | ± 2140.12K | ops/s |
| prometheusInc | 68.57K | ± 573.58 | ops/s |
| prometheusNoLabelsInc | 64.54K | ± 3.71K | ops/s |
| codahaleIncNoLabels | 59.37K | ± 643.37 | ops/s |
| prometheusAdd | 56.76K | ± 659.63 | ops/s |
| openTelemetryBoundInc | 53.42K | ± 764.24 | ops/s |
| openTelemetryBoundAdd | 48.09K | ± 759.03 | ops/s |
| openTelemetryIncNoLabels | 36.64K | ± 340.00 | ops/s |
| openTelemetryInc | 29.50K | ± 662.11 | ops/s |
| openTelemetryAdd | 25.56K | ± 723.99 | ops/s |
| simpleclientInc | 10.76K | ± 168.64 | ops/s |
| simpleclientNoLabelsInc | 10.52K | ± 470.49 | ops/s |
| simpleclientAdd | 10.42K | ± 270.45 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 15.27K | ± 219.84 | ops/s |
| prometheusClassic | 9.49K | ± 751.26 | ops/s |
| openTelemetryClassic | 8.29K | ± 860.22 | ops/s |
| simpleclient | 6.94K | ± 256.16 | ops/s |
| openTelemetryBoundClassic | 6.74K | ± 2.43K | ops/s |
| prometheusNative | 5.02K | ± 67.15 | ops/s |
| prometheusClassicSingleThread | 4.50K | ± 38.77 | ops/s |
| openTelemetryBoundExponential | 1.20K | ± 79.41 | ops/s |
| openTelemetryExponential | 972.49 | ± 37.52 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| openMetricsWriteToNull | 33.37K | ± 393.18 | ops/s |
| prometheusWriteToNull | 33.35K | ± 668.25 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToByteArray | 834.93K | ± 23.72K | ops/s |
| prometheusWriteToNull | 830.80K | ± 60.84K | ops/s |
| openMetricsWriteToByteArray | 739.55K | ± 38.05K | ops/s |
| openMetricsWriteToNull | 708.99K | ± 10.46K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.016 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.037 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.019 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.018 | — | — |
| CounterBenchmark.openTelemetryInc | 0.032 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.026 | — | — |
| CounterBenchmark.prometheusAdd | 0.065 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.054 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.057 | — | — |
| CounterBenchmark.simpleclientAdd | 0.090 | — | — |
| CounterBenchmark.simpleclientInc | 0.087 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.089 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.156 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.788 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.116 | — | — |
| HistogramBenchmark.openTelemetryExponential | 0.968 | — | — |
| HistogramBenchmark.prometheusClassic | 0.391 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.526 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.606 | — | — |
| HistogramBenchmark.prometheusNative | 417712.741 | — | — |
| HistogramBenchmark.simpleclient | 0.135 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.105 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.105 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18429.334 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18448.001 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      59369.663    ± 643.374  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      25555.747    ± 723.994  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      48090.771    ± 759.029  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      53415.544    ± 764.240  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      29495.566    ± 662.112  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      36644.605    ± 339.996  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      56764.335    ± 659.634  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  723183029.189 ± 15173000.949  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  216472285.376 ± 2193277.753  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      68573.471    ± 573.575  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  207887167.029 ± 4059312.850  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   95140836.377 ± 2140116.130  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      64542.814   ± 3708.707  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15      10421.261    ± 270.448  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15      10757.397    ± 168.644  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15      10518.058    ± 470.489  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       6738.598   ± 2427.046  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1202.752     ± 79.413  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       8292.288    ± 860.216  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        972.493     ± 37.518  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       9493.048    ± 751.263  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      15274.178    ± 219.842  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4495.832     ± 38.774  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       5019.027     ± 67.145  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       6944.887    ± 256.157  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      33372.937    ± 393.180  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      33351.006    ± 668.247  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     739548.217  ± 38054.773  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     708993.262  ± 10458.367  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     834925.995  ± 23724.434  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     830797.627  ± 60840.406  ops/s
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
