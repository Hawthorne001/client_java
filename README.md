# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-22T17:34:32Z
- **Commit:** [`a483539`](https://github.com/Hawthorne001/client_java/commit/a4835397c5fe237a534bd9c3259827d7e3e38d31)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.82K | ± 1.88K | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.34K | ± 107.96 | ops/s | 1.1x slower |
| prometheusAdd | 51.09K | ± 645.99 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 46.86K | ± 3.35K | ops/s | 1.4x slower |
| simpleclientInc | 6.78K | ± 16.98 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.57K | ± 218.28 | ops/s | 10x slower |
| simpleclientAdd | 6.22K | ± 245.62 | ops/s | 11x slower |
| openTelemetryInc | 1.33K | ± 180.61 | ops/s | 49x slower |
| openTelemetryAdd | 1.30K | ± 38.12 | ops/s | 51x slower |
| openTelemetryIncNoLabels | 1.18K | ± 61.72 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.09K | ± 1.81K | ops/s | **fastest** |
| simpleclient | 4.55K | ± 37.52 | ops/s | 1.1x slower |
| prometheusNative | 2.98K | ± 230.07 | ops/s | 1.7x slower |
| openTelemetryClassic | 684.30 | ± 16.39 | ops/s | 7.4x slower |
| openTelemetryExponential | 524.26 | ± 17.02 | ops/s | 9.7x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 497.22K | ± 1.92K | ops/s | **fastest** |
| prometheusWriteToByteArray | 492.89K | ± 1.64K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 488.95K | ± 6.86K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.88K | ± 5.31K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      46863.961   ± 3352.751  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1303.328     ± 38.121  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1334.173    ± 180.606  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1184.476     ± 61.716  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51087.338    ± 645.989  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65823.591   ± 1881.060  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57339.564    ± 107.956  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6224.068    ± 245.621  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6781.707     ± 16.979  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6573.136    ± 218.275  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        684.302     ± 16.394  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        524.255     ± 17.016  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5094.133   ± 1809.654  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2976.878    ± 230.070  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4552.776     ± 37.523  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     488946.601   ± 6860.370  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485877.089   ± 5311.034  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492885.357   ± 1635.731  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     497218.058   ± 1917.030  ops/s
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
