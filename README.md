# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-30T09:23:11Z
- **Commit:** [`2a2c73d`](https://github.com/Hawthorne001/client_java/commit/2a2c73d7d23bfa291b10df85056027398e8a868d)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 64.53K | ± 1.50K | ops/s | **fastest** |
| prometheusNoLabelsInc | 56.78K | ± 312.34 | ops/s | 1.1x slower |
| prometheusAdd | 50.98K | ± 382.12 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.14K | ± 1.53K | ops/s | 1.3x slower |
| simpleclientInc | 6.56K | ± 43.41 | ops/s | 9.8x slower |
| simpleclientNoLabelsInc | 6.45K | ± 113.22 | ops/s | 10x slower |
| simpleclientAdd | 6.31K | ± 236.99 | ops/s | 10x slower |
| openTelemetryIncNoLabels | 3.29K | ± 227.28 | ops/s | 20x slower |
| openTelemetryAdd | 2.88K | ± 161.87 | ops/s | 22x slower |
| openTelemetryInc | 2.87K | ± 144.76 | ops/s | 22x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 4.52K | ± 550.89 | ops/s | **fastest** |
| simpleclient | 4.31K | ± 155.34 | ops/s | 1.0x slower |
| prometheusNative | 2.81K | ± 366.44 | ops/s | 1.6x slower |
| openTelemetryClassic | 739.59 | ± 31.88 | ops/s | 6.1x slower |
| openTelemetryExponential | 649.43 | ± 61.15 | ops/s | 7.0x slower |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| openMetricsWriteToNull | 24.23K | ± 943.84 | ops/s | **fastest** |
| prometheusWriteToNull | 23.07K | ± 475.43 | ops/s | 1.1x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 494.72K | ± 4.52K | ops/s | **fastest** |
| prometheusWriteToNull | 494.30K | ± 7.48K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 483.98K | ± 3.85K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 476.06K | ± 2.38K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48142.913   ± 1526.795  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       2880.298    ± 161.871  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       2869.449    ± 144.761  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       3291.828    ± 227.279  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50983.307    ± 382.117  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64526.046   ± 1500.942  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56780.517    ± 312.343  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6307.988    ± 236.991  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6559.265     ± 43.406  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6448.768    ± 113.221  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        739.590     ± 31.881  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        649.427     ± 61.150  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       4519.536    ± 550.889  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2812.068    ± 366.442  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4314.291    ± 155.344  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      24230.611    ± 943.841  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      23065.204    ± 475.430  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     476060.050   ± 2381.648  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     483984.157   ± 3853.665  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     494716.979   ± 4515.526  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     494300.412   ± 7479.383  ops/s
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
