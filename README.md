# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-10-07T10:19:13Z
- **Commit:** [`ba050b0`](https://github.com/Hawthorne001/client_java/commit/ba050b022f6e06203df318a7871b744cc4d6a167)
- **JDK:** 25.0.3 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 1/4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results for PR head

### CounterBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusCachedLabelValuesInc | 545.17M | ± 6508.40K | ops/s |
| prometheusCachedLabelValuesIncSingleThread | 334.65M | ± 471.26K | ops/s |
| prometheusLabelValuesInc | 117.40M | ± 2103.02K | ops/s |
| prometheusLabelValuesIncSingleThread | 58.44M | ± 320.74K | ops/s |
| prometheusInc | 64.96K | ± 1.05K | ops/s |
| prometheusNoLabelsInc | 56.74K | ± 232.69 | ops/s |
| prometheusAdd | 50.93K | ± 587.29 | ops/s |
| codahaleIncNoLabels | 49.34K | ± 1.31K | ops/s |
| openTelemetryBoundInc | 37.68K | ± 65.79 | ops/s |
| openTelemetryBoundAdd | 31.87K | ± 194.13 | ops/s |
| openTelemetryIncNoLabels | 22.68K | ± 1.14K | ops/s |
| openTelemetryInc | 18.05K | ± 53.93 | ops/s |
| openTelemetryAdd | 15.41K | ± 209.38 | ops/s |
| simpleclientAdd | 6.44K | ± 13.16 | ops/s |
| simpleclientInc | 6.41K | ± 148.32 | ops/s |
| simpleclientNoLabelsInc | 6.35K | ± 42.01 | ops/s |

### HistogramBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusClassicPerThread | 12.04K | ± 26.45 | ops/s |
| prometheusClassic | 5.83K | ± 1.50K | ops/s |
| openTelemetryBoundClassic | 5.06K | ± 1.69K | ops/s |
| prometheusClassicSingleThread | 4.54K | ± 14.97 | ops/s |
| simpleclient | 4.36K | ± 38.55 | ops/s |
| openTelemetryClassic | 4.09K | ± 264.96 | ops/s |
| prometheusNative | 2.79K | ± 311.56 | ops/s |
| openTelemetryBoundExponential | 1.01K | ± 109.37 | ops/s |
| openTelemetryExponential | 863.05 | ± 21.32 | ops/s |

### HistogramTextFormatBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 24.04K | ± 283.84 | ops/s |
| openMetricsWriteToNull | 23.46K | ± 269.56 | ops/s |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units |
|:----------|------:|------:|:------|
| prometheusWriteToNull | 549.50K | ± 4.70K | ops/s |
| prometheusWriteToByteArray | 548.60K | ± 3.28K | ops/s |
| openMetricsWriteToNull | 524.89K | ± 7.19K | ops/s |
| openMetricsWriteToByteArray | 511.29K | ± 5.24K | ops/s |

## Allocation per operation

JMH GC profiler `gc.alloc.rate.norm`, in bytes per benchmark operation (lower is better).
Delta is PR minus base, shown only for matching benchmark configurations. Values are descriptive, not statistical regression verdicts; — means unavailable or not comparable. Each benchmark defines its own operation.

| Benchmark | PR B/op | Base B/op | Delta B/op |
|:----------|--------:|----------:|-----------:|
| CounterBenchmark.codahaleIncNoLabels | 0.019 | — | — |
| CounterBenchmark.openTelemetryAdd | 0.060 | — | — |
| CounterBenchmark.openTelemetryBoundAdd | 0.029 | — | — |
| CounterBenchmark.openTelemetryBoundInc | 0.025 | — | — |
| CounterBenchmark.openTelemetryInc | 0.051 | — | — |
| CounterBenchmark.openTelemetryIncNoLabels | 0.041 | — | — |
| CounterBenchmark.prometheusAdd | 0.072 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesInc | 0.000 | — | — |
| CounterBenchmark.prometheusCachedLabelValuesIncSingleThread | 0.000 | — | — |
| CounterBenchmark.prometheusInc | 0.057 | — | — |
| CounterBenchmark.prometheusLabelValuesInc | 48.000 | — | — |
| CounterBenchmark.prometheusLabelValuesIncSingleThread | 48.000 | — | — |
| CounterBenchmark.prometheusNoLabelsInc | 0.065 | — | — |
| CounterBenchmark.simpleclientAdd | 0.144 | — | — |
| CounterBenchmark.simpleclientInc | 0.145 | — | — |
| CounterBenchmark.simpleclientNoLabelsInc | 0.146 | — | — |
| HistogramBenchmark.openTelemetryBoundClassic | 0.196 | — | — |
| HistogramBenchmark.openTelemetryBoundExponential | 0.932 | — | — |
| HistogramBenchmark.openTelemetryClassic | 0.231 | — | — |
| HistogramBenchmark.openTelemetryExponential | 1.074 | — | — |
| HistogramBenchmark.prometheusClassic | 0.676 | — | — |
| HistogramBenchmark.prometheusClassicPerThread | 0.657 | — | — |
| HistogramBenchmark.prometheusClassicSingleThread | 0.642 | — | — |
| HistogramBenchmark.prometheusNative | 335793.340 | — | — |
| HistogramBenchmark.simpleclient | 0.214 | — | — |
| HistogramTextFormatBenchmark.openMetricsWriteToNull | 43648.149 | — | — |
| HistogramTextFormatBenchmark.prometheusWriteToNull | 43648.146 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToByteArray | 18424.001 | — | — |
| TextFormatUtilBenchmark.openMetricsWriteToNull | 18424.001 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToByteArray | 18429.335 | — | — |
| TextFormatUtilBenchmark.prometheusWriteToNull | 18410.668 | — | — |

### Raw Results

```text
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      49340.716   ± 1309.946  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15      15412.160    ± 209.376  ops/s
CounterBenchmark.openTelemetryBoundAdd              thrpt   15      31870.492    ± 194.130  ops/s
CounterBenchmark.openTelemetryBoundInc              thrpt   15      37675.145     ± 65.787  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15      18054.989     ± 53.931  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15      22682.620   ± 1137.606  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      50926.975    ± 587.293  ops/s
CounterBenchmark.prometheusCachedLabelValuesInc     thrpt   15  545173224.825 ± 6508399.682  ops/s
CounterBenchmark.prometheusCachedLabelValuesIncSingleThread  thrpt   15  334652649.050 ± 471260.725  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      64958.156   ± 1053.884  ops/s
CounterBenchmark.prometheusLabelValuesInc           thrpt   15  117402223.353 ± 2103023.378  ops/s
CounterBenchmark.prometheusLabelValuesIncSingleThread  thrpt   15   58438594.293 ± 320736.516  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      56743.107    ± 232.693  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6435.349     ± 13.159  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6410.780    ± 148.321  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6350.152     ± 42.011  ops/s
HistogramBenchmark.openTelemetryBoundClassic        thrpt   15       5062.181   ± 1693.070  ops/s
HistogramBenchmark.openTelemetryBoundExponential    thrpt   15       1005.899    ± 109.375  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15       4090.937    ± 264.957  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        863.054     ± 21.322  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5829.590   ± 1501.917  ops/s
HistogramBenchmark.prometheusClassicPerThread       thrpt   15      12042.808     ± 26.446  ops/s
HistogramBenchmark.prometheusClassicSingleThread    thrpt   15       4539.309     ± 14.972  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2785.400    ± 311.560  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4355.538     ± 38.555  ops/s
HistogramTextFormatBenchmark.openMetricsWriteToNull  thrpt   15      23463.455    ± 269.561  ops/s
HistogramTextFormatBenchmark.prometheusWriteToNull  thrpt   15      24035.843    ± 283.844  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     511285.477   ± 5239.587  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     524894.583   ± 7192.412  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     548596.963   ± 3283.500  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     549495.815   ± 4697.099  ops/s
```

## Notes

- **Score** = the JMH primary metric; throughput is higher-is-better and latency is lower-is-better.
- **Error** = 99.9% confidence interval
- Scores for different benchmark methods are not ranked against one another; they may measure different workloads.

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter updates and label-value lookup (selected methods only) |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |
