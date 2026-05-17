# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-17T18:16:21Z
- **Commit:** [`94b33b7`](https://github.com/Hawthorne001/client_java/commit/94b33b7527ce21b12ff2a3f9cd23c63cdb42e274)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.49K | ± 1.81K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.98K | ± 96.40 | ops/s | 1.1x slower |
| prometheusAdd | 51.18K | ± 255.53 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 47.78K | ± 2.93K | ops/s | 1.4x slower |
| simpleclientInc | 6.58K | ± 6.57 | ops/s | 9.9x slower |
| simpleclientNoLabelsInc | 6.37K | ± 51.87 | ops/s | 10x slower |
| simpleclientAdd | 6.37K | ± 211.83 | ops/s | 10x slower |
| openTelemetryInc | 3.57K | ± 158.07 | ops/s | 18x slower |
| openTelemetryIncNoLabels | 3.43K | ± 261.30 | ops/s | 19x slower |
| openTelemetryAdd | 3.07K | ± 59.58 | ops/s | 21x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.64K | ± 1.12K | ops/s | **fastest** |
| simpleclient | 4.40K | ± 67.38 | ops/s | 1.3x slower |
| prometheusNative | 2.69K | ± 68.80 | ops/s | 2.1x slower |
| openTelemetryClassic | 778.46 | ± 17.40 | ops/s | 7.2x slower |
| openTelemetryExponential | 622.08 | ± 93.45 | ops/s | 9.1x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 24.03K | ± 67.11 | ops/s | **fastest** |
| openMetricsWriteToNull | 23.73K | ± 168.61 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 511.82K | ± 7.22K | ops/s | **fastest** |
| prometheusWriteToByteArray | 502.62K | ± 3.37K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 488.13K | ± 1.10K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 484.41K | ± 3.81K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      47779.023   ± 2930.632  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3072.268     ± 59.580  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3574.958    ± 158.069  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3427.964    ± 261.295  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51177.407    ± 255.532  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65487.616   ± 1805.103  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56977.524     ± 96.403  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6365.008    ± 211.829  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6583.031      ± 6.566  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6373.230     ± 51.868  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        778.463     ± 17.397  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        622.082     ± 93.451  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5636.207   ± 1120.573  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2689.586     ± 68.799  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4399.822     ± 67.376  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23734.709    ± 168.610  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24026.056     ± 67.112  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     484405.125   ± 3805.106  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     488130.288   ± 1101.929  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     502624.312   ± 3368.833  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     511822.615   ± 7221.103  ops/s
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
