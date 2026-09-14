# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-13T17:17:29Z
- **Commit:** [`fcc4466`](https://github.com/Hawthorne001/client_java/commit/fcc4466e36262d155e3f7b0211fd8da6b013e3af)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusInc | 76.43K | ± 684.40 | ops/s |
| prometheusNoLabelsInc | 66.98K | ± 1.04K | ops/s |
| prometheusAdd | 61.75K | ± 748.92 | ops/s |
| codahaleIncNoLabels | 55.55K | ± 2.49K | ops/s |
| openTelemetryIncNoLabels | 22.09K | ± 51.86 | ops/s |
| openTelemetryInc | 17.80K | ± 128.79 | ops/s |
| openTelemetryAdd | 15.76K | ± 65.35 | ops/s |
| simpleclientInc | 7.95K | ± 78.71 | ops/s |
| simpleclientNoLabelsInc | 7.74K | ± 242.78 | ops/s |
| simpleclientAdd | 7.73K | ± 182.37 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 17.65K | ± 127.38 | ops/s |
| prometheusClassicSingleThread | 7.55K | ± 12.86 | ops/s |
| prometheusClassic | 6.67K | ± 1.92K | ops/s |
| simpleclient | 5.89K | ± 41.38 | ops/s |
| prometheusNative | 3.49K | ± 155.17 | ops/s |
| openTelemetryClassic | 1.03K | ± 134.59 | ops/s |
| openTelemetryExponential | 875.09 | ± 39.32 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 35.47K | ± 146.61 | ops/s |
| openMetricsWriteToNull | 35.41K | ± 223.39 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 708.78K | ± 6.18K | ops/s |
| prometheusWriteToByteArray | 694.26K | ± 9.59K | ops/s |
| openMetricsWriteToByteArray | 648.44K | ± 2.96K | ops/s |
| openMetricsWriteToNull | 623.82K | ± 17.24K | ops/s |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      55549.424   ± 2487.108  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15758.880     ± 65.349  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      17801.962    ± 128.788  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22086.901     ± 51.857  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      61753.234    ± 748.922  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      76425.003    ± 684.396  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      66981.918   ± 1044.798  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7732.230    ± 182.372  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7949.461     ± 78.714  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7741.781    ± 242.779  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       1029.542    ± 134.593  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        875.090     ± 39.323  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6665.816   ± 1921.369  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      17652.490    ± 127.383  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       7552.026     ± 12.862  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3485.237    ± 155.168  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5891.238     ± 41.380  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      35410.473    ± 223.395  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      35465.990    ± 146.605  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     648443.905   ± 2962.539  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     623823.211  ± 17236.130  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     694259.668   ± 9587.758  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     708777.433   ± 6183.233  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
