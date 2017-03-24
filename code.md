# ²é¿´Í¼Æ¬ÇÐ»»½Ç¶È

    public static int checkDeviceAutoRotateBitmap(String photoPath) {
        try {
            switch (new ExifInterface(photoPath).getAttributeInt("Orientation", 1)) {
                case 3:
                    LogUtils.LogError("ORIENTATION_ROTATE_180", "ORIENTATION_ROTATE_180");
                    return 180;
                case 6:
                    LogUtils.LogError("ORIENTATION_ROTATE_90", "ORIENTATION_ROTATE_90");
                    return 90;
                default:
                    LogUtils.LogError("checkDeviceAutoRotateBitmap", "default default default default");
                    return 0;
            }
        } catch (Exception e) {
            e.printStackTrace();
            return 0;
        }
    }