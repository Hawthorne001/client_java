# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-27T06:43:45Z
- **Commit:** [`dec8e5b`](https://github.com/Hawthorne001/client_java/commit/dec8e5b15a1c48c54be6b81517f2cb334bc0ee60)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1010-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 75.48K | ± 3.72K | ops/s | **fastest** |
| prometheusNoLabelsInc | 67.02K | ± 641.57 | ops/s | 1.1x slower |
| prometheusAdd | 60.91K | ± 1.33K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 56.48K | ± 2.37K | ops/s | 1.3x slower |
| simpleclientInc | 7.80K | ± 242.60 | ops/s | 9.7x slower |
| openTelemetryInc | 7.78K | ± 301.61 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 7.65K | ± 319.99 | ops/s | 9.9x slower |
| simpleclientAdd | 7.60K | ± 241.54 | ops/s | 9.9x slower |
| openTelemetryIncNoLabels | 7.09K | ± 761.05 | ops/s | 11x slower |
| openTelemetryAdd | 5.96K | ± 1.03K | ops/s | 13x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.48K | ± 367.72 | ops/s | **fastest** |
| simpleclient | 5.69K | ± 65.49 | ops/s | 1.1x slower |
| prometheusNative | 4.01K | ± 231.62 | ops/s | 1.6x slower |
| openTelemetryClassic | 923.92 | ± 18.76 | ops/s | 7.0x slower |
| openTelemetryExponential | 726.09 | ± 40.07 | ops/s | 8.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 681.44K | ± 10.19K | ops/s | **fastest** |
| prometheusWriteToByteArray | 661.25K | ± 7.97K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 652.08K | ± 5.75K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 635.97K | ± 6.86K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      56478.150   ± 2368.373  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       5964.594   ± 1028.424  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       7781.125    ± 301.606  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       7092.464    ± 761.045  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      60905.786   ± 1326.931  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      75480.778   ± 3722.476  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      67019.960    ± 641.571  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       7604.876    ± 241.542  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7800.444    ± 242.598  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7645.242    ± 319.986  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        923.915     ± 18.765  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        726.088     ± 40.066  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6477.162    ± 367.723  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       4005.269    ± 231.621  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       5686.283     ± 65.491  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     635973.583   ± 6856.730  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     652084.813   ± 5746.853  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     661249.466   ± 7974.385  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     681440.944  ± 10189.650  ops/s
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
