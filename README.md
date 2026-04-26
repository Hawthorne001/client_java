# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-26T05:39:26Z
- **Commit:** [`e898720`](https://github.com/Hawthorne001/client_java/commit/e898720958021b1e81753f3cce45aa9ce5bfdca0)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 59.84K | ± 242.59 | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.78K | ± 711.33 | ops/s | 1.2x slower |
| prometheusAdd | 48.74K | ± 1.03K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 43.11K | ± 1.13K | ops/s | 1.4x slower |
| simpleclientInc | 6.27K | ± 60.44 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.16K | ± 161.76 | ops/s | 9.7x slower |
| simpleclientAdd | 5.84K | ± 265.92 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 4.83K | ± 923.27 | ops/s | 12x slower |
| openTelemetryInc | 4.59K | ± 1.13K | ops/s | 13x slower |
| openTelemetryAdd | 3.42K | ± 191.62 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 7.09K | ± 1.14K | ops/s | **fastest** |
| simpleclient | 4.38K | ± 29.97 | ops/s | 1.6x slower |
| prometheusNative | 2.87K | ± 260.01 | ops/s | 2.5x slower |
| openTelemetryClassic | 725.21 | ± 13.02 | ops/s | 9.8x slower |
| openTelemetryExponential | 520.71 | ± 6.01 | ops/s | 14x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 557.74K | ± 2.57K | ops/s | **fastest** |
| prometheusWriteToByteArray | 553.38K | ± 2.72K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 538.10K | ± 5.50K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 524.50K | ± 3.28K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      43107.024   ± 1127.071  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3419.823    ± 191.625  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4585.366   ± 1126.874  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4830.554    ± 923.270  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48735.662   ± 1033.107  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      59836.088    ± 242.592  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51775.399    ± 711.327  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5839.433    ± 265.917  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6274.846     ± 60.439  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6162.256    ± 161.764  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        725.214     ± 13.024  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        520.710      ± 6.011  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       7093.930   ± 1135.770  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2871.550    ± 260.006  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4384.332     ± 29.965  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     524499.870   ± 3284.594  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     538099.737   ± 5499.534  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     553378.395   ± 2719.716  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     557735.257   ± 2568.557  ops/s
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
