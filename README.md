# MachineLearingInAction
机器学习源代码
package com.hthk.dt.billing.reporting.sam;

import com.hthk.dt.billing.reporting.ExcelProcessUtils;
import com.hthk.dt.billing.reporting.domain.DataBean;
import org.apache.poi.hssf.usermodel.HSSFWorkbook;
import org.apache.poi.ss.usermodel.Workbook;
import org.junit.Test;
import org.springframework.boot.test.context.SpringBootTest;

import java.math.BigDecimal;
import java.util.ArrayList;
import java.util.List;

/**
 * @Author: samccs
 * @Date: 2020/5/15 上午 11:07
 * @Version 1.0
 */
@SpringBootTest
public class ExcelTest {

    @Test
    public void test01(){
        String path = "src\\main\\resources\\mytest.xlsx";
        Workbook workBook = ExcelProcessUtils.getWorkBook(path);
        List<DataBean> dataBeans = ExcelProcessUtils.parseExcel(workBook, DataBean.class);
        System.out.println(dataBeans);

    }

    @Test
    public void test02(){
        try {
            DataBean dataBean = new DataBean();
            dataBean.setPLMN("APPMM_MO");
            dataBean.setRoamingPartner("ACCSEE");
            dataBean.setCountry("CHINA");
            dataBean.setTotalAmount(new BigDecimal("3024.225"));
            List<DataBean> dataBeans = new ArrayList<>();
            dataBeans.add(dataBean);
            String path = "src\\main\\resources\\mytest01.xls";
            String sheetName = "GL_INFO";
            String sheetName2 = "GL_INFO_2";
            HSSFWorkbook workbook = new HSSFWorkbook();
            ExcelProcessUtils.writerExcel(workbook,dataBeans,path,sheetName);
            ExcelProcessUtils.writerExcel(workbook,dataBeans,path,sheetName2);
            workbook.close();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }


    }
}
