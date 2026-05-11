# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-11T13:51:11Z
- **Commit:** [`11cb921`](https://github.com/Hawthorne001/client_java/commit/11cb921cdea4789cf86ca903867ce9e3e5debe9e)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.12K | ± 628.03 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.18K | ± 367.60 | ops/s | 1.2x slower |
| prometheusAdd | 47.51K | ± 559.69 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.25K | ± 291.77 | ops/s | 1.3x slower |
| simpleclientInc | 6.15K | ± 111.24 | ops/s | 9.6x slower |
| simpleclientAdd | 6.11K | ± 26.04 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 5.85K | ± 72.92 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.38K | ± 805.21 | ops/s | 11x slower |
| openTelemetryInc | 3.80K | ± 310.10 | ops/s | 16x slower |
| openTelemetryAdd | 3.37K | ± 151.86 | ops/s | 18x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.16K | ± 1.64K | ops/s | **fastest** |
| simpleclient | 4.53K | ± 63.62 | ops/s | 1.6x slower |
| prometheusNative | 2.81K | ± 247.99 | ops/s | 2.5x slower |
| openTelemetryClassic | 689.09 | ± 7.45 | ops/s | 10x slower |
| openTelemetryExponential | 531.39 | ± 9.13 | ops/s | 13x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.32K | ± 401.80 | ops/s | **fastest** |
| openMetricsWriteToNull | 26.76K | ± 520.89 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.95K | ± 9.60K | ops/s | **fastest** |
| prometheusWriteToByteArray | 549.18K | ± 2.28K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 525.20K | ± 8.64K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 518.37K | ± 10.56K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44246.046    ± 291.765  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3367.321    ± 151.856  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3802.200    ± 310.098  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5377.239    ± 805.213  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47508.941    ± 559.695  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59117.351    ± 628.029  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51175.501    ± 367.598  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6108.409     ± 26.036  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6148.564    ± 111.236  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       5850.906     ± 72.923  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        689.085      ± 7.447  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        531.393      ± 9.134  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7160.258   ± 1642.740  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2814.478    ± 247.989  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4528.275     ± 63.617  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      26763.322    ± 520.892  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27318.602    ± 401.797  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     518370.952  ± 10555.696  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     525204.225   ± 8636.613  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     549175.698   ± 2280.239  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556954.482   ± 9604.367  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
