# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-24T22:32:12Z
- **Commit:** [`5ee188f`](https://github.com/Hawthorne001/client_java/commit/5ee188ff288806f76e53a89d32431a93bb53da11)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 58.25K | ± 1.78K | ops/s | **fastest** |
| prometheusNoLabelsInc | 51.56K | ± 511.17 | ops/s | 1.1x slower |
| prometheusAdd | 48.74K | ± 515.50 | ops/s | 1.2x slower |
| codahaleIncNoLabels | 42.76K | ± 971.85 | ops/s | 1.4x slower |
| simpleclientInc | 6.11K | ± 80.96 | ops/s | 9.5x slower |
| simpleclientNoLabelsInc | 6.04K | ± 182.14 | ops/s | 9.6x slower |
| simpleclientAdd | 5.66K | ± 236.35 | ops/s | 10x slower |
| openTelemetryInc | 4.66K | ± 920.09 | ops/s | 12x slower |
| openTelemetryIncNoLabels | 4.02K | ± 257.30 | ops/s | 14x slower |
| openTelemetryAdd | 3.51K | ± 92.85 | ops/s | 17x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.08K | ± 2.52K | ops/s | **fastest** |
| simpleclient | 4.32K | ± 35.70 | ops/s | 1.4x slower |
| prometheusNative | 3.09K | ± 183.47 | ops/s | 2.0x slower |
| openTelemetryClassic | 717.20 | ± 20.42 | ops/s | 8.5x slower |
| openTelemetryExponential | 551.32 | ± 20.89 | ops/s | 11x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 27.57K | ± 164.48 | ops/s | **fastest** |
| openMetricsWriteToNull | 27.05K | ± 405.81 | ops/s | 1.0x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 579.25K | ± 7.45K | ops/s | **fastest** |
| prometheusWriteToByteArray | 572.14K | ± 4.74K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 550.34K | ± 4.90K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 537.04K | ± 2.80K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      42759.797    ± 971.850  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       3506.469     ± 92.846  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       4663.670    ± 920.088  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       4019.060    ± 257.299  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48741.649    ± 515.499  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      58247.518   ± 1781.712  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      51563.401    ± 511.175  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5664.860    ± 236.353  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6108.845     ± 80.964  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6036.737    ± 182.143  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        717.198     ± 20.420  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        551.319     ± 20.888  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6076.288   ± 2518.583  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3088.445    ± 183.469  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4318.004     ± 35.695  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      27054.860    ± 405.812  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      27570.974    ± 164.483  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     537044.678   ± 2800.296  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     550342.074   ± 4901.327  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     572144.092   ± 4742.264  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     579252.131   ± 7446.316  ops/s
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
