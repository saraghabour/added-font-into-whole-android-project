# added-font-into-whole-android-project
import new font not found into  application with create new folder (assets) 

public class TypeFaceUtil {


    public static void overrideFont(Context context,String defaultFontNameToOverride,
                                    String customFontFileNameInAssets){

        final Typeface typeface = Typeface.createFromAsset(context.getAssets(),
                customFontFileNameInAssets);

        if (Build.VERSION.SDK_INT>=Build.VERSION_CODES.LOLLIPOP){
            Map<String,Typeface> typefaceMap = new HashMap<String,Typeface>();

            typefaceMap.put("Serif",typeface);
            try {
                final Field field = Typeface.class.getDeclaredField("sSystemFontMap");
                field.setAccessible(true);
                field.set(null,typefaceMap);
            } catch (IllegalAccessException e) {
                e.printStackTrace();
            } catch (NoSuchFieldException e) {
                e.printStackTrace();
            }
        }else{
            try {

                final Field defaultfontType = Typeface.class.getDeclaredField(defaultFontNameToOverride);
                defaultfontType.setAccessible(true);
                defaultfontType.set(null, typeface);
            } catch (IllegalAccessException e) {
                e.printStackTrace();
            } catch (NoSuchFieldException e) {
                e.printStackTrace();
            }
        }

    }
}
