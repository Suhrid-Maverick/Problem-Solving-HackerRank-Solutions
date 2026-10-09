import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.List;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Scanner;
import java.util.Set;

public class Solution {
    static boolean[] P = new boolean[62];

    static final long MOD = (long) Math.pow(10, 9) + 7l;
    static Map<Integer, ThreeDigit> DIGITMAP = new HashMap<Integer, ThreeDigit>();
    static Map<Long, Long> tab = new HashMap<Long, Long>();

    static long[] depNUM = new long[400001];
    static int NL = 400005;

    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();

        P[2] = true;
        P[3] = true;
        List<Integer> list = new ArrayList<Integer>();
        list.add(2);
        list.add(3);

        for (int i = 5; i < 50; i += 6) {
            int i1 = i;
            int i2 = i + 2;
            boolean bi1 = true;
            boolean bi2 = true;
            int se = (int) Math.sqrt(i2);

            for (int p : list) {
                if (i1 % p == 0)
                    bi1 = false;
                if (i2 % p == 0)
                    bi2 = false;
                if (p > se) {
                    break;
                }
                if (!bi1 && !bi2)
                    break;
            }
            if (bi1) {
                P[i1] = true;
                list.add(i1);
            }
            if (bi2) {
                P[i2] = true;
                list.add(i2);
            }

        }

        for (int i = 2; i < 1000; i++) {
            int temp = i / 100 + i / 10 % 10 + i % 10;

            if (P[temp]) {
                DIGITMAP.put(i, new ThreeDigit(i));
            }
        }
        for (ThreeDigit td : DIGITMAP.values()) {
            initDigit(td);
        }

        Map<Integer, Long> fourNums = new HashMap<Integer, Long>();
        ThreeDigit[] tds = new ThreeDigit[1000];
        int[] depSum = new int[NL + 1];
        for (ThreeDigit td : DIGITMAP.values()) {
            if (td.v > 100) {
                fourNums.put(td.v, 1l);
                depSum[3]++;
            }  
            tds[td.v] = td;
        }
        depSum[1] = 9;
        depSum[2] = 90;
        for (int i = 4; i <= NL; i++) {
            Map<Integer, Long> fourNums2 = new HashMap<Integer, Long>();
            travel(fourNums, fourNums2, tds, depSum, i);
            fourNums = fourNums2;
        }

        while (N-- > 0) {
            System.out.println(depSum[sc.nextInt()]);
        }
        sc.close();
    }

    public static void travel(Map<Integer, Long> fourNums, Map<Integer, Long> fourNums2, ThreeDigit[] tds, int[] depSum,
            int dep) {

        for (Entry<Integer, Long> entry : fourNums.entrySet()) {
            int fourNum = entry.getKey();
            long num = entry.getValue();
            int first = fourNum / 1000;
            ThreeDigit td = tds[fourNum % 1000];
            for (ThreeDigit ttd : td.set) {
                if (P[first + td.threeSum + ttd.last]) {
                    depSum[dep] += num;
                    depSum[dep] %= MOD;
                    Long v = fourNums2.get(td.v * 10 + ttd.last);
                    if (v == null)
                        fourNums2.put(td.v * 10 + ttd.last, num);
                    else
                        fourNums2.put(td.v * 10 + ttd.last, (v + num) % MOD);

                }
            }
        }

    }

    public static void initDigit(ThreeDigit td) {
        for (int i = 0; i < 10; i++) {
            if (P[td.threeSum + i] && P[td.twoSum + i]) {
                ThreeDigit gettd = DIGITMAP.get(td.v % 100 * 10 + i);
                if (!td.set.contains(gettd)) {
                    td.set.add(gettd);
                }
            }
        }
    }

    public static class ThreeDigit {
        private int v;
        private int threeSum;
        private int twoSum;
        private int first;
        private int last;
        private Set<ThreeDigit> set = new HashSet<ThreeDigit>();

        public void addNextDigit() {

        }

        public ThreeDigit(int v) {
            this.v = v;
            this.last = v % 10;
            this.twoSum = this.last + v / 10 % 10;
            this.threeSum = this.twoSum + v / 100;
            this.first = this.v / 100;
        }

        public int hashCode() {
            return this.v;
        }

        public boolean equals(Object o) {
            ThreeDigit o1 = (ThreeDigit) o;
            return this.v == o1.v;
        }
    }
}
