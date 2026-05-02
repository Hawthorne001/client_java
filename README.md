# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-02T11:21:25Z
- **Commit:** [`188e434`](https://github.com/Hawthorne001/client_java/commit/188e434f25be73f75a463239b5cb4d54a8f72cca)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 66.00K | ± 358.73 | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.99K | ± 791.71 | ops/s | 1.2x slower |
| prometheusAdd | 50.62K | ± 1.31K | ops/s | 1.3x slower |
| codahaleIncNoLabels | 50.18K | ± 109.21 | ops/s | 1.3x slower |
| simpleclientInc | 6.54K | ± 162.21 | ops/s | 10x slower |
| simpleclientNoLabelsInc | 6.47K | ± 170.32 | ops/s | 10x slower |
| simpleclientAdd | 6.46K | ± 22.57 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.52K | ± 344.73 | ops/s | 19x slower |
| openTelemetryInc | 3.52K | ± 451.41 | ops/s | 19x slower |
| openTelemetryAdd | 3.35K | ± 289.40 | ops/s | 20x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.66K | ± 1.39K | ops/s | **fastest** |
| simpleclient | 4.44K | ± 11.01 | ops/s | 1.3x slower |
| prometheusNative | 3.07K | ± 305.40 | ops/s | 1.8x slower |
| openTelemetryClassic | 774.43 | ± 25.57 | ops/s | 7.3x slower |
| openTelemetryExponential | 640.50 | ± 50.62 | ops/s | 8.8x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 490.17K | ± 6.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 479.35K | ± 5.55K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 477.53K | ± 4.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 473.25K | ± 1.93K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      50184.112    ± 109.207  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3351.294    ± 289.404  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       3515.297    ± 451.414  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3521.142    ± 344.727  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50618.989   ± 1313.136  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      66003.398    ± 358.730  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55993.322    ± 791.706  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6464.431     ± 22.569  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6541.700    ± 162.214  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6468.254    ± 170.316  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        774.435     ± 25.571  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        640.501     ± 50.623  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5663.186   ± 1390.611  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3065.876    ± 305.399  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4440.632     ± 11.008  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     473245.347   ± 1932.016  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     477530.298   ± 4613.062  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     479347.921   ± 5551.807  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     490165.969   ± 6454.728  ops/s
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
