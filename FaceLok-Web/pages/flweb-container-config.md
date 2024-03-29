![Ipsidy](../../images/authid.png)
# Proof/Verified Web - FaceLok Web Container Configuration

FaceLok Web container provides ability to configure some of the behavior settings when running “On-Premises”. Below is the list of supported options listed as environment variables.

| Variable Name | Description | Default Value |
| ------------- | ----------- | ------------- |
| UsePathBase | For running behind reverse-proxies that do not support URL-rewriting and pass prefixed request path use `UsePathBase` parameter so that application can extract and re-apply the prefix when serving requests. | |
| IDLive__Url | ID R&D’s IDLive™ Face integration is enabled by specifying URL to the running service instance. | |
| IDLive__Threshold | Liveness threshold value that allows IDLive Face image verification to pass. | 0.40 |
| IDComplete__Url | URL to IDComplete server instance for image verification integration. When IDComplete integration is enabled client applications need to pass IDComplete Operation ID and one time secret in the "SourceOperationId" field in "idc:OperationId:OneTimeSecret" format. | |
| IDComplete__Username | IDComplete Username for additional application authentication | |
| IDComplete__Password | IDComplete Password for additional application authentication | |
| Redis__Config | Service depends on Redis service version 5 or higher. At minimum set variable to the host name of the Redis host and (possible) authentication values:<br> Redis__Config="redis_host:6379,password=secret"<br> For more detailed configuration string options check https://stackexchange.github.io/StackExchange.Redis/Configuration article.
| Redis__KeyPrefix | Configures Redis key prefix that container should use when storing values in the DB. | “flwa:” |
| Limits__MaxSessionsPerSourceOperationId | Enables session limiting mechanism based on Redis OperationId tracking. <br> When Limits__MaxSessionsPerSourceOperationId is set to non-zero value, each POST of api/LivenessTest requires client to pass SourceOperationId field in the body JSON.<br> Service will then check if Redis DB contains "OperationId-{SourceOperationId}" (no prefix is used) hash key and only allow further processing when such key exists.<br> Additionally, service will increment "flwa-sessions" field in the specified (hash) key and only continue if total count of sessions is below Limits__MaxSessionsPerSourceOperationId value. | 0 |
| Limits__MaxSessionTime | Specifies number of seconds after which session is automatically cleaned-up. | 600 |
| Limits__MaxKeyFrames | Specifies amount of high-resolution images backend will pull from each client session to pass liveness. | 3 |
| AIConfig__FaceThreshold | For experimental/development purposes these recognition tuning parameters are available for changing during start-up. Normally these should not be changed. | 0.5 |
| AIConfig__SmileThreshold | | 0 |
| AIConfig__BlinkThreshold | | 0.7 |
| AIConfig__SamplingWindow | | 120 |
| AIConfig__MinFaceSize | | 250 |
| AIConfig__SmileDelta | | 1 |
| LightMeter__BrightnessThreshold | | 250 |
| LightMeter__HotSpotThreshold | | 0.5 |
| LightMeter__HistScoreThreshold | | 1.1 |
| Debug__KeyFrameTtl | Sets Redis high resolution frame key expiration time (in seconds) so that images are kept in the memory for longer time. | 0 |
| Debug__ExposeLandmarks | Expose detected face outlines and probability values in response JSON for visualization in client overlays. | true |
| Debug__ExposeScoring | Expose liveness scoring in response JSON to client for visualization in debug overlays. | false |

#

[Back to Main Page](../README.md)