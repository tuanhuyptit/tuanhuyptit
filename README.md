/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package scaling;

/**
 *
 * @author Tuan Huy Vu
 */
import java.io.File;
import java.io.IOException;
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
public class Scaling {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        // TODO code application logic here
          BufferedImage img = null;
        File f = null;

        // read image
        try {
            f = new File("D:\\cat.bmp");
            img = ImageIO.read(f);
        } catch (IOException e) {
            System.out.println(e);
        }

        /* get pixel value */
        System.out.println(img.getHeight() + "x" + img.getWidth());
         for(int i = 0; i < img.getHeight()/2; i++){
            for(int j = 0; j < img.getWidth()/2; j++){
                int p;
                p = img.getRGB(i*2, j*2);

                //get alpha
               int a = (p >> 24) & 0xff;

//                // get red
                int r = (p >> 16) & 0xff;
//
//                // get green
                int g = (p >> 8) & 0xff;
//
//                // get blue
                int b = p & 0xff;

                /*
                for simplicity we will set the ARGB
                value to 255, 100, 150 and 200 respectively.
                */
            a = 255;
              r = 100;
              g = 150;
               b = 200;

                // set the pixel value
                p = (a << 24) | (r << 16) | (g << 8) | b;
                if(i*2 + 1 < img.getWidth()){
                    img.setRGB(i*2 + 1, j*2, p);
                }    
                if(j*2 + 1 < img.getHeight()){
                    img.setRGB(i*2, j*2 + 1, p);
                }    
                if(i*2 + 1 < img.getWidth() && j*2 + 1 < img.getHeight()){
                    img.setRGB(i*2 + 1, j*2 + 1, p);
                }    
            }
        }
         //write image
        try {
            f = new File("D:\\catOut.bmp");
            ImageIO.write(img, "bmp", f);
        } catch (IOException e) {
            System.out.println(e);
        }

    }
    
}
