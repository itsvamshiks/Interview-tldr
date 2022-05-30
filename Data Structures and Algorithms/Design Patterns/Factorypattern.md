## Factory Pattern



```

abstract class Plan{
    protected double rate;
    abstract void getRate();
    
    public void calculateBill(int units){
        System.out.println(units*rate);
    }
}

class DomesticPlan extends Plan{
    public void getRate(){
        rate = 3.5;
    }
}

class CommercialPlan extends Plan{
    public void getRate(){
        rate = 7.5;
    }
}


class GetPlanFactory{
    public Plan getPlan(String planType){
        if(planType == null)
            return null;
        
        if(planType.equalsIgnoreCase("DOMESTIC PLAN")){
            return new DomesticPlan();
        }
        
        if(planType.equalsIgnoreCase("COMMERCIAL PLAN")){
            return new CommercialPlan();
        }
        
        return null;
    }

}

class GenerateBill{
    public static void main(String[] args){
        GetPlanFactory planFactory = new GetPlanFactory();
        String planName = args[0];
        
        Plan p = planFactory.getPlan(planName);
        
        System.out.println(p.getRate() + "  " + p.calculateBill(units));
    }

}

```
