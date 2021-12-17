### JAVA 中 DES 加解密代码示例

一、简介
DES 是对称性加密里面常见一种，全称为 Data Encryption Standard，即数据加密标准，是一种使用密钥加密的块算法。密钥长度是64位(bit)，超过位数密钥被忽略。所谓对称性加密即加密和解密密钥相同，对称性加密一般会按照固定长度，把待加密字符串分成块，不足一整块或者刚好最后有特殊填充字符。

跨语言做 DES 加密解密经常会出现问题，往往是填充方式不对、编码不一致或者加密解密模式没有对应上造成。常见的填充模式有： pkcs5、pkcs7、iso10126、ansix923、zero。加密模式有：DES-ECB、DES-CBC、DES-CTR、DES-OFB、DES-CFB。

作为一个软件开发者，可以通过工具测试 DES 加密解密，这里推荐一个在线工具：
http://tool.chacuo.net/cryptdes

二、`java`实现,文件名：`DesEncrypter.java`
```java
import javax.crypto.Cipher;
import javax.crypto.SecretKey;
import javax.crypto.SecretKeyFactory;
import javax.crypto.spec.DESKeySpec;
import javax.crypto.spec.IvParameterSpec;


/**
 * DES加密算法工具类
 * `key`和`iv`是一样的
 * 可以自行设置
 * @author someone
 * @version 1.0
 */
public class DesEncrypter {
    private static final String key = "youkeykey";

    /**
     * 加密方法，对指定的str加密
     *
     * @param str
     * @return
     */
    public String encrypt(String str) throws Exception {
        Cipher cipher;
        cipher = Cipher.getInstance("DES/CBC/PKCS5Padding");

        DESKeySpec desKeySpec = new DESKeySpec(key.getBytes("UTF-8"));

        SecretKeyFactory keyFactory = SecretKeyFactory.getInstance("DES");
        SecretKey secretKey = keyFactory.generateSecret(desKeySpec);
        IvParameterSpec iv = new IvParameterSpec(key.getBytes("UTF-8"));
        cipher.init(Cipher.ENCRYPT_MODE, secretKey, iv);

        byte[] strs = cipher.doFinal(str.getBytes("UTF-8"));
        return bytesToString(strs);

    }

    /**
     * 解密算法，对指定str解密
     *
     * @param str
     * @return
     */
    public String decrypt(String str) throws Exception {
        byte[] bytesrc = stringToBytes(str);
        Cipher cipher = Cipher.getInstance("DES/CBC/PKCS5Padding");
        DESKeySpec desKeySpec = new DESKeySpec(key.getBytes("UTF-8"));
        SecretKeyFactory keyFactory = SecretKeyFactory.getInstance("DES");
        SecretKey secretKey = keyFactory.generateSecret(desKeySpec);
        IvParameterSpec iv = new IvParameterSpec(key.getBytes("UTF-8"));

        cipher.init(Cipher.DECRYPT_MODE, secretKey, iv);

        byte[] retByte = cipher.doFinal(bytesrc);
        return new String(retByte, "UTF-8");
    }

    //Byte数组转String
    public static String bytesToString(byte b[]) {
        StringBuffer hexString = new StringBuffer();
        for (int i = 0; i < b.length; i++) {
            String plainText = Integer.toHexString(0xff & b[i]);
            if (plainText.length() < 2)
                plainText = "0" + plainText;
            hexString.append(plainText);
        }

        return hexString.toString();
    }

    //String转Byte数组
    public static byte[] stringToBytes(String temp) {
        byte digest[] = new byte[temp.length() / 2];
        for (int i = 0; i < digest.length; i++) {
            String byteString = temp.substring(2 * i, 2 * i + 2);
            int byteValue = Integer.parseInt(byteString, 16);
            digest[i] = (byte) byteValue;
        }

        return digest;
    }
}
```

三、调用示例,文件名：`Main.java`
```java
public class Main {

    /**
     * 测试
     *
     * @param args
     */
    public static void main(String[] args) {
        try {
            DesEncrypter desEncrypter = new DesEncrypter();
            String value = "123456";
            System.out.println("加密的数据:" + value);
            String a = desEncrypter.encrypt(value);
            System.out.println("加密后的数据:" + a);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```