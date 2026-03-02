# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-03-02T21:59:44Z
- **Commit:** [`6938479`](https://github.com/Hawthorne001/client_java/commit/69384791685f0e86a28f04191434ecab310365ba)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.14.0-1017-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.15K | ± 2.85K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.24K | ± 76.74 | ops/s | 1.1x slower |
| prometheusAdd | 51.30K | ± 406.31 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.40K | ± 1.57K | ops/s | 1.3x slower |
| simpleclientInc | 6.76K | ± 34.50 | ops/s | 9.6x slower |
| simpleclientNoLabelsInc | 6.57K | ± 204.45 | ops/s | 9.9x slower |
| simpleclientAdd | 6.26K | ± 177.31 | ops/s | 10x slower |
| openTelemetryInc | 1.38K | ± 123.26 | ops/s | 47x slower |
| openTelemetryAdd | 1.30K | ± 14.08 | ops/s | 50x slower |
| openTelemetryIncNoLabels | 1.25K | ± 62.45 | ops/s | 52x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.06K | ± 1.01K | ops/s | **fastest** |
| simpleclient | 4.51K | ± 104.51 | ops/s | 1.1x slower |
| prometheusNative | 2.94K | ± 425.40 | ops/s | 1.7x slower |
| openTelemetryClassic | 703.89 | ± 83.41 | ops/s | 7.2x slower |
| openTelemetryExponential | 520.62 | ± 7.23 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 495.65K | ± 2.42K | ops/s | **fastest** |
| prometheusWriteToByteArray | 482.99K | ± 5.80K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 472.37K | ± 4.15K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 468.97K | ± 7.48K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48395.199   ± 1573.201  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1302.097     ± 14.083  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1383.221    ± 123.255  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1245.133     ± 62.448  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51300.170    ± 406.309  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65151.069   ± 2853.086  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57244.805     ± 76.743  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6258.766    ± 177.310  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6758.877     ± 34.495  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6566.606    ± 204.449  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        703.894     ± 83.413  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        520.620      ± 7.232  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5062.276   ± 1007.926  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2942.268    ± 425.397  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4514.076    ± 104.512  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     472369.908   ± 4152.013  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     468968.460   ± 7484.313  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     482990.550   ± 5804.445  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     495651.855   ± 2417.889  ops/s
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
