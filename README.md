# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-04-23T04:42:13Z
- **Commit:** [`4b69f40`](https://github.com/Hawthorne001/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1011-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.95K | ± 1.01K | ops/s | **fastest** |
| prometheusAdd | 50.96K | ± 618.44 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 49.70K | ± 968.06 | ops/s | 1.3x slower |
| prometheusNoLabelsInc | 44.88K | ± 17.62K | ops/s | 1.4x slower |
| simpleclientInc | 6.66K | ± 68.91 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.36K | ± 9.64 | ops/s | 10x slower |
| simpleclientAdd | 6.07K | ± 299.87 | ops/s | 11x slower |
| openTelemetryInc | 1.36K | ± 231.14 | ops/s | 48x slower |
| openTelemetryIncNoLabels | 1.31K | ± 191.86 | ops/s | 50x slower |
| openTelemetryAdd | 1.27K | ± 47.80 | ops/s | 51x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.45K | ± 540.54 | ops/s | **fastest** |
| simpleclient | 4.40K | ± 77.75 | ops/s | 1.2x slower |
| prometheusNative | 2.93K | ± 335.83 | ops/s | 1.9x slower |
| openTelemetryClassic | 697.13 | ± 23.06 | ops/s | 7.8x slower |
| openTelemetryExponential | 544.23 | ± 18.88 | ops/s | 10x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 466.68K | ± 4.48K | ops/s | **fastest** |
| prometheusWriteToNull | 464.35K | ± 7.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 459.64K | ± 6.71K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 457.62K | ± 2.16K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49696.535    ± 968.061  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1273.079     ± 47.796  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1359.605    ± 231.142  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1310.033    ± 191.861  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50964.893    ± 618.436  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64947.525   ± 1006.764  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      44883.231  ± 17624.636  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6069.756    ± 299.868  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6664.025     ± 68.909  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6360.732      ± 9.639  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        697.127     ± 23.060  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        544.227     ± 18.883  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5446.107    ± 540.536  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2928.854    ± 335.833  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4402.236     ± 77.751  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     457617.406   ± 2164.303  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     459639.812   ± 6711.782  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     466682.273   ± 4484.824  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     464347.133   ± 7657.120  ops/s
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
