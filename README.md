# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-14T14:52:39Z
- **Commit:** [`d50be82`](https://github.com/Hawthorne001/client_java/commit/d50be827046c0547e0e534569480bf349e0c3376)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.40K | ± 294.58 | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.40K | ± 931.70 | ops/s | 1.2x slower |
| prometheusAdd | 51.58K | ± 283.36 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.05K | ± 1.96K | ops/s | 1.4x slower |
| simpleclientInc | 6.74K | ± 20.61 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.56K | ± 201.40 | ops/s | 10x slower |
| simpleclientAdd | 6.24K | ± 198.41 | ops/s | 11x slower |
| openTelemetryAdd | 1.45K | ± 303.06 | ops/s | 46x slower |
| openTelemetryInc | 1.34K | ± 190.35 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.19K | ± 38.64 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.20K | ± 1.16K | ops/s | **fastest** |
| simpleclient | 4.57K | ± 21.80 | ops/s | 1.6x slower |
| prometheusNative | 3.19K | ± 46.27 | ops/s | 2.3x slower |
| openTelemetryClassic | 650.17 | ± 26.87 | ops/s | 11x slower |
| openTelemetryExponential | 558.72 | ± 12.13 | ops/s | 13x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 487.78K | ± 3.14K | ops/s | **fastest** |
| prometheusWriteToByteArray | 485.21K | ± 2.18K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 479.16K | ± 3.46K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.46K | ± 2.45K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48052.880   ± 1964.457  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1449.465    ± 303.055  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1341.723    ± 190.351  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1194.610     ± 38.638  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51576.140    ± 283.355  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66397.177    ± 294.581  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56397.689    ± 931.697  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6235.748    ± 198.410  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6737.535     ± 20.613  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6557.943    ± 201.397  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        650.166     ± 26.867  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        558.716     ± 12.126  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7196.199   ± 1157.124  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3192.128     ± 46.271  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4566.881     ± 21.798  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473459.608   ± 2449.649  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     479158.267   ± 3457.444  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     485208.735   ± 2183.228  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     487778.144   ± 3141.474  ops/s
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
