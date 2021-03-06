# Python을 이용한 객체 지향 프로그래밍 \(2\)

## 과제 내용 설명 <a id="&#xACFC;&#xC81C;-&#xB0B4;&#xC6A9;-&#xC124;&#xBA85;"></a>

DataLoader 예제를 더 발전시켜서 MydataLoader2를 만들어 봅시다. data를 하나 더 늘려서 data1과 data2를 인자로 받습니다.

1. data1과 data2의 각 value를 제곱 하는 기능을 만들어 봅시다.\(make\_square\) ex. data1 = \[1,2,3\] -&gt; make\_square -&gt; \[1,4,9\]
2. shuffle 기능을 data1, data2 둘다 섞을 수 있도록 바꿉니다.
3. for loop가 돌 때마다 i번째 data1의 값과 data2의 값을 더한 값을 인쇄할 수 있게 바꿔봅시다. ex. data1 = \[1,9,4\] data2 = \[4,1,9\] -&gt; \[5,10,13\]을 하나씩 리턴

## 우수과제 선정 이유 <a id="&#xC6B0;&#xC218;&#xACFC;&#xC81C;-&#xC120;&#xC815;-&#xC774;&#xC720;"></a>

깔끔한 코드에 상세한 주석으로 선정하게 되었습니다

## 기존 Dataloader <a id="&#xAE30;&#xC874;-Dataloader"></a>

In \[2\]:

```python
import random
class MyDataLoader:
    def __init__(self, data):
        self.size = len(data) 
        self.data = data
        
    def __iter__(self): 
        self.index = 0
        return self
 
    def __next__(self):
        if self.index >= self.size:
            raise StopIteration
        n = self.data[self.index]
        self.index += 1
        return n
    
    def shuffle(self):
        random.shuffle(self.data)
```

In \[3\]:

```python
import random
class MyDataLoader2:
    def __init__(self, data1, data2):
        # data1과 data2 크기는 같다고 가정합시다
        self.size = len(data1) 
        self.data1 = data1
        self.data2 = data2
        # 두 데이터가 필요하므로 각각 data1, data2를 인자로 받도록
        # data2 추가!
        
 
    # __iter__에서는 나를 반환해주고 __next__에서는 for loop가
    # 돌떄마다 인쇄하고 싶은 값을 리턴합니다.
    def __iter__(self): 
        self.index = 0
        return self #나를 반환해야하므로 return값은 self!
 
    def __next__(self):
        ##################
        #data1과 data2를 더해서 리턴할 수 있는 iterator를 완성해주세요
        if self.index >= self.size:
            raise StopIteration 
            
        n1=self.data1[self.index]
        n2=self.data2[self.index]
        
        self.index +=1         
        return n1 + n2 
        #iter, next가 for loop와 같은 기능을 하는데 
        #next에서는 돌때마다 인쇄하고 싶은 값을 반환하므로, 
        #data1과 data2의 index에 해당하는 값을 각각 더한 값을 return값으로 받음
    def shuffle(self):
        #########
        # data1과 data2를 shuffle해주세요
        random.shuffle(self.data1) #random.shuffle을 통해 data1과 data2를 shuffle!
        random.shuffle(self.data2)
        #########
    def make_square(self):
        ######### 
        # data1과 data2의 값들을 다 제곱해주세요!
        self.data1 = [x**2 for x in self.data1] # data안의 값들을 모두 제곱해주었숩나다
        self.data2 = [x**2 for x in self.data2]
        #########
```

In \[5\]:

```python
# data1과 data2 크기는 같다고 가정합시다
loader = MyDataLoader2([i for i in range(300)], [i for i in range(300)])
loader.make_square() ## data1과 data2를 제곱할 수 있는 method를 완성해주세요!
loader.shuffle()
for i, x in enumerate(loader): # for loop 가 도니까 __iter__
    print(f"{i} : {x}")
```

```text
0 : 6793
1 : 123029
2 : 94165
3 : 124690
4 : 122777
5 : 28193
6 : 65952
7 : 40324
8 : 126617
9 : 76921
10 : 103346
11 : 42137
12 : 61605
13 : 36725
14 : 126113
15 : 57157
16 : 18064
17 : 14825
18 : 170
19 : 107705
20 : 17642
21 : 24680
22 : 51354
23 : 54641
24 : 41229
25 : 13960
26 : 65809
27 : 2557
28 : 39301
29 : 148850
30 : 81509
31 : 30420
32 : 22608
33 : 24946
34 : 31618
35 : 145850
36 : 22100
37 : 24993
38 : 99556
39 : 156245
40 : 1609
41 : 102177
42 : 17221
43 : 129785
44 : 34625
45 : 68002
46 : 629
47 : 24400
48 : 7969
49 : 46864
50 : 9556
51 : 1913
52 : 62281
53 : 85450
54 : 18481
55 : 69241
56 : 63706
57 : 141508
58 : 39584
59 : 35066
60 : 115048
61 : 90944
62 : 116570
63 : 59986
64 : 25373
65 : 78938
66 : 94994
67 : 84338
68 : 61492
69 : 112538
70 : 63433
71 : 33293
72 : 59666
73 : 59240
74 : 45481
75 : 65594
76 : 32365
77 : 53012
78 : 78250
79 : 53252
80 : 116285
81 : 85892
82 : 3725
83 : 100676
84 : 97722
85 : 21709
86 : 118340
87 : 134674
88 : 51860
89 : 84005
90 : 32733
91 : 873
92 : 58194
93 : 1156
94 : 89069
95 : 53873
96 : 31850
97 : 977
98 : 40229
99 : 25040
100 : 75332
101 : 85178
102 : 83656
103 : 30325
104 : 118586
105 : 63162
106 : 11554
107 : 108040
108 : 149
109 : 50576
110 : 122029
111 : 98009
112 : 91717
113 : 43570
114 : 162
115 : 66064
116 : 34850
117 : 92426
118 : 19682
119 : 61960
120 : 86309
121 : 46458
122 : 74528
123 : 74752
124 : 5402
125 : 5513
126 : 34081
127 : 85322
128 : 64234
129 : 86437
130 : 83528
131 : 27380
132 : 106625
133 : 8450
134 : 71245
135 : 64609
136 : 65602
137 : 72922
138 : 13669
139 : 120200
140 : 55933
141 : 31613
142 : 39586
143 : 129364
144 : 16488
145 : 105026
146 : 55828
147 : 107258
148 : 72189
149 : 21465
150 : 161905
151 : 8660
152 : 88769
153 : 80660
154 : 73193
155 : 5330
156 : 102629
157 : 50389
158 : 63058
159 : 119650
160 : 50569
161 : 43137
162 : 112234
163 : 87050
164 : 1649
165 : 23524
166 : 160180
167 : 20852
168 : 51316
169 : 7873
170 : 35162
171 : 97949
172 : 77589
173 : 69205
174 : 21601
175 : 95290
176 : 63725
177 : 32740
178 : 9445
179 : 68429
180 : 143690
181 : 30276
182 : 32701
183 : 84752
184 : 119345
185 : 112969
186 : 59060
187 : 36490
188 : 88328
189 : 60941
190 : 75280
191 : 67093
192 : 58925
193 : 89896
194 : 13085
195 : 86413
196 : 2041
197 : 1565
198 : 3529
199 : 57565
200 : 79429
201 : 26353
202 : 9661
203 : 51082
204 : 28465
205 : 108245
206 : 15809
207 : 20228
208 : 94945
209 : 174641
210 : 104980
211 : 6452
212 : 49300
213 : 92770
214 : 98317
215 : 70178
216 : 26977
217 : 101124
218 : 78665
219 : 67546
220 : 69301
221 : 30482
222 : 90481
223 : 40708
224 : 26792
225 : 19634
226 : 78676
227 : 11108
228 : 33317
229 : 96298
230 : 63306
231 : 52180
232 : 797
233 : 93025
234 : 19625
235 : 90810
236 : 92745
237 : 63202
238 : 69929
239 : 71849
240 : 16385
241 : 7272
242 : 40925
243 : 2708
244 : 18173
245 : 34772
246 : 84608
247 : 60680
248 : 72361
249 : 82882
250 : 102818
251 : 52450
252 : 13225
253 : 143226
254 : 3712
255 : 57301
256 : 154277
257 : 13285
258 : 124309
259 : 99397
260 : 84906
261 : 3050
262 : 37993
263 : 83458
264 : 93041
265 : 63729
266 : 21425
267 : 27145
268 : 8936
269 : 35594
270 : 77285
271 : 56101
272 : 79402
273 : 14900
274 : 82948
275 : 1412
276 : 1037
277 : 110905
278 : 103300
279 : 2610
280 : 106290
281 : 118612
282 : 81541
283 : 16250
284 : 57924
285 : 38504
286 : 48682
287 : 6290
288 : 97250
289 : 6625
290 : 16250
291 : 41410
292 : 52900
293 : 70249
294 : 30213
295 : 79285
296 : 121472
297 : 58372
298 : 27045
299 : 74880
```

