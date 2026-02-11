# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-02-11T12:55:26Z
- **Commit:** [`04bc727`](https://github.com/Hawthorne001/client_java/commit/04bc727fcb2b9ba4da8eb7268c562f5385f5eda4)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.11.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.95K | ± 820.38 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.21K | ± 242.52 | ops/s | 1.2x slower |
| prometheusAdd | 51.08K | ± 686.76 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.78K | ± 1.35K | ops/s | 1.4x slower |
| simpleclientInc | 6.77K | ± 19.28 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.63K | ± 137.94 | ops/s | 10x slower |
| simpleclientAdd | 6.30K | ± 103.69 | ops/s | 11x slower |
| openTelemetryInc | 1.27K | ± 24.42 | ops/s | 53x slower |
| openTelemetryAdd | 1.23K | ± 12.02 | ops/s | 55x slower |
| openTelemetryIncNoLabels | 1.20K | ± 57.44 | ops/s | 56x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.91K | ± 777.28 | ops/s | **fastest** |
| simpleclient | 4.55K | ± 26.47 | ops/s | 1.1x slower |
| prometheusNative | 3.05K | ± 283.12 | ops/s | 1.6x slower |
| openTelemetryClassic | 651.38 | ± 6.07 | ops/s | 7.5x slower |
| openTelemetryExponential | 554.44 | ± 6.27 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 492.41K | ± 4.08K | ops/s | **fastest** |
| prometheusWriteToNull | 490.96K | ± 2.44K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 485.72K | ± 4.18K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 482.25K | ± 4.53K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48775.823   ± 1351.399  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1226.308     ± 12.017  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1265.465     ± 24.416  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1199.880     ± 57.435  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51080.291    ± 686.763  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66948.934    ± 820.382  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57213.690    ± 242.519  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6299.432    ± 103.686  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6769.164     ± 19.276  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6626.869    ± 137.941  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        651.382      ± 6.068  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        554.442      ± 6.266  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4907.975    ± 777.280  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3049.496    ± 283.125  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4546.135     ± 26.474  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     482248.672   ± 4525.508  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     485723.777   ± 4178.044  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     492414.401   ± 4075.204  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490963.319   ± 2437.511  ops/s
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
