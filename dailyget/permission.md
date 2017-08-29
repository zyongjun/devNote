#### 应用intent安装权限问题：
intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);

最终安装apk的代码变成这样:


public static void installApk(Context context, String apkPath) {
    if (context == null || TextUtils.isEmpty(apkPath)) {
        return;
    }


    File file = new File(apkPath);
    Intent intent = new Intent(Intent.ACTION_VIEW);

    //判读版本是否在7.0以上
    if (Build.VERSION.SDK_INT >= 24) {
        //provider authorities
        Uri apkUri = FileProvider.getUriForFile(context, "com.mydomain.fileprovider", file);
        //Granting Temporary Permissions to a URI
        intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
        intent.setDataAndType(apkUri, "application/vnd.android.package-archive");
    } else {
        intent.setDataAndType(Uri.fromFile(file), "application/vnd.android.package-archive");
    }

    context.startActivity(intent);
}