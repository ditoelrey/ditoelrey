Димитар Ахтаров, бр. на индекс 223268

Control flow graph

![TGraf drawio](https://github.com/ditoelrey/ditoelrey/assets/138317237/def1299a-1829-4ef8-869c-88c25d04f304)

Цикломатска комплексност - 10
E - N + 2 = 31 - 23 + 2 = 10

23 - јазли
31 - ребра

Тестови :

class SILab2Test {
    private List<Item> items(Item... elems){
        return new ArrayList<>(Arrays.asList(elems));
    }


    @Test
    void EveryBranchTest(){
        Item item_invalid_barcode = new Item("Shower Gel", "ssdesxas", 100, 0);
        Item item_no_barcode = new Item("Shower Gel", null, 100, 0);
        Item item_valid = new Item("Shower Gel", "123123123", 100, 0);
        Item item_high_price_discount_starting_with_zero = new Item("Shampoo", "0123456789", 500, 0.1f);

        RuntimeException ex;
        ex = assertThrows(RuntimeException.class, () -> SILab2.checkCart(null, 0));
        assertTrue(ex.getMessage().contains("allItems list can't be null!"));

        ex = assertThrows(RuntimeException.class, () -> SILab2.checkCart(items(item_invalid_barcode), 0));
        assertTrue(ex.getMessage().contains("Invalid character in item barcode!"));

        ex = assertThrows(RuntimeException.class, () -> SILab2.checkCart(items(item_no_barcode), 0));
        assertTrue(ex.getMessage().contains("No barcode!"));

        assertEquals(true, SILab2.checkCart(items(item_valid), 300));
        assertEquals(false, SILab2.checkCart(items(item_valid), 50));

        assertTrue(SILab2.checkCart(items(item_high_price_discount_starting_with_zero), 1000));
    }




    @Test
    void MultipleConditionTest(){
        //(item.getPrice() > 300 && item.getDiscount() > 0 && item.getBarcode().charAt(0) == '0')

        //T && T && T
        Item TTT = new Item(null,"0003",500,0.1f);

        assertTrue(TTT.getPrice() > 300);
        assertTrue(TTT.getDiscount() > 0);
        assertEquals('0', TTT.getBarcode().charAt(0));

        //T && T && F
        Item TTF = new Item(null,"5000",550,0.1f);

        assertTrue(TTF.getPrice() > 300);
        assertTrue(TTF.getDiscount() > 0);
        assertNotEquals('0', TTF.getBarcode().charAt(0));

        //T && F...
        Item TF = new Item(null,"2223",550,0);

        assertTrue(TF.getPrice() > 300);
        assertFalse(TF.getDiscount() > 0);

        //F ...
        Item F = new Item(null,"2223",5,0);

        assertFalse(F.getPrice() > 300);
    }

}

Овие unit тестови ги проверуваат различните аспекти на функцијата checkCart во класата SILab2, која има за цел да провери дали кошничката за купување е валидна.

EveryBranchTest:

Невалидни влезни параметри: Тестира дали функцијата се однесува соодветно при проследување на невалидни влезни параметри, како null за листа на артикли или артикл со невалиден баркод.
Валидни сценарија: Ги тестира различните можни комбинации на влезните параметри, како што се валиден артикл со баркод, цена и попуст.
MultipleConditionTest:

Ги тестира различните комбинации на услови што се проверуваат во функцијата checkCart. Секој тест креира специфичен артикл и проверува дали функцијата враќа соодветен резултат во зависност од состојбата на артиклот.



