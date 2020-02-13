# Error 14e5336f-cf56-41d9-8862-f02789d370f3

This error may occur in GuzabaPlatform\Platform\Application\GuzabaPlatform::__construct() if there is mismatch of the languages in the configuration.
The defined GuzabaPlatform::CONFIG_RUNTIME['target_language'] is not found in the array GuzabaPlatform::CONFIG_RUNTIME['supported_languages].
To correct this error add the target_language in the supported_languages array or set the supported_languages array to empty or completely remove this element from the configuration array.