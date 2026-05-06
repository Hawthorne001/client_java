# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-06T12:32:50Z
- **Commit:** [`e7ef068`](https://github.com/Hawthorne001/client_java/commit/e7ef068d1a42acf9ea07e351d44f3559dd78cbe8)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.50K | ± 552.93 | ops/s | **fastest** |
| prometheusAdd | 47.93K | ± 84.46 | ops/s | 1.3x slower |
| prometheusNoLabelsInc | 46.77K | ± 8.02K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 43.13K | ± 1.00K | ops/s | 1.4x slower |
| simpleclientNoLabelsInc | 6.27K | ± 24.42 | ops/s | 9.6x slower |
| simpleclientInc | 6.26K | ± 52.59 | ops/s | 9.7x slower |
| simpleclientAdd | 6.00K | ± 130.18 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 5.43K | ± 865.51 | ops/s | 11x slower |
| openTelemetryInc | 4.87K | ± 965.00 | ops/s | 12x slower |
| openTelemetryAdd | 4.01K | ± 790.58 | ops/s | 15x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.53K | ± 1.49K | ops/s | **fastest** |
| simpleclient | 4.16K | ± 35.50 | ops/s | 1.3x slower |
| prometheusNative | 3.07K | ± 139.61 | ops/s | 1.8x slower |
| openTelemetryClassic | 773.80 | ± 24.28 | ops/s | 7.1x slower |
| openTelemetryExponential | 563.88 | ± 25.54 | ops/s | 9.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 556.13K | ± 6.96K | ops/s | **fastest** |
| prometheusWriteToByteArray | 544.63K | ± 5.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 539.20K | ± 5.19K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 519.67K | ± 3.11K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43130.124   ± 1000.740  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       4010.291    ± 790.576  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4872.972    ± 965.004  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       5427.493    ± 865.515  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      47928.306     ± 84.459  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60504.475    ± 552.931  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      46772.691   ± 8023.697  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5995.924    ± 130.181  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6261.927     ± 52.588  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6272.600     ± 24.423  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        773.803     ± 24.278  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        563.880     ± 25.542  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5529.793   ± 1489.067  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3068.960    ± 139.610  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4164.099     ± 35.502  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     519667.061   ± 3110.053  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     539201.611   ± 5193.844  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     544634.014   ± 5545.165  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     556130.218   ± 6960.575  ops/s
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
