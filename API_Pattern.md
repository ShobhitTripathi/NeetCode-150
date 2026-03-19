Here’s your **API Call Questionnaire Template in clean Markdown format** — ready to copy into notes / GitHub / Obsidian.

---

````markdown
#  API Call Problem Template (HackerRank Style)

##  Problem Pattern

Almost all API-based questions follow this pipeline:

1. Call API (handle pagination)
2. Parse JSON response
3. Filter / Transform data
4. Aggregate / Sort results
5. Return final output

---

##  Java Template (Reusable)

```java
import java.io.*;
import java.net.*;
import java.util.*;
import org.json.*;

class Solution {

    public static List<String> solve(String baseUrl) {
        List<String> result = new ArrayList<>();

        int page = 1;
        int totalPages = 1;

        try {
            while (page <= totalPages) {
                String response = callApi(baseUrl + "?page=" + page);

                JSONObject json = new JSONObject(response);
                totalPages = json.getInt("total_pages");

                JSONArray data = json.getJSONArray("data");

                for (int i = 0; i < data.length(); i++) {
                    JSONObject obj = data.getJSONObject(i);

                    // Extract fields (modify per problem)
                    String name = obj.optString("name");
                    int value = obj.optInt("value");

                    // Apply condition
                    if (value > 50) {
                        result.add(name);
                    }
                }

                page++;
            }

        } catch (Exception e) {
            e.printStackTrace();
        }

        // Final processing
        Collections.sort(result);

        return result;
    }

    private static String callApi(String urlStr) throws Exception {
        URL url = new URL(urlStr);
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();

        conn.setRequestMethod("GET");
        conn.setConnectTimeout(5000);
        conn.setReadTimeout(5000);

        BufferedReader reader = new BufferedReader(
                new InputStreamReader(conn.getInputStream())
        );

        StringBuilder response = new StringBuilder();
        String line;

        while ((line = reader.readLine()) != null) {
            response.append(line);
        }

        reader.close();

        return response.toString();
    }
}
````

---

##  Common Variations

###  1. Find Max / Min

```java
int max = Integer.MIN_VALUE;

for (...) {
    int val = obj.getInt("score");
    max = Math.max(max, val);
}
```

---

###  2. Group By (Aggregation)

```java
Map<String, Integer> map = new HashMap<>();

for (...) {
    String key = obj.getString("team");
    int val = obj.getInt("goals");

    map.put(key, map.getOrDefault(key, 0) + val);
}
```

---

###  3. Top K Elements (Heap)

```java
PriorityQueue<String> pq = new PriorityQueue<>(
    (a, b) -> b.compareTo(a)
);
```

---

###  4. Custom Sorting

```java
Collections.sort(result, (a, b) -> a.length() - b.length());
```

---

##  Standard API Response Format

```json
{
  "page": 1,
  "per_page": 10,
  "total": 50,
  "total_pages": 5,
  "data": [
    {
      "name": "abc",
      "value": 100
    }
  ]
}
```

---

##  Edge Cases to Handle

* Empty data array
* Missing fields → use `optString`, `optInt`
* API timeout / failure
* Large data (avoid storing everything if not required)

---

##  Complexity Discussion

* Time Complexity: `O(N log N)` (if sorting)
* Space Complexity: `O(N)` (depends on storage)

### Optimization Ideas:

* Process data on-the-fly (streaming)
* Avoid unnecessary storage
* Use efficient data structures (heap/map)

---

##  Interview Explanation Template

> I will paginate through the API using `total_pages`, parse each response, extract required fields, apply filtering conditions, and aggregate results. Finally, I will sort or format the output as required.

---

##  Pro Tips

* Always check `total_pages`
* Use `optXXX()` instead of `getXXX()`
* Avoid multiple API calls unnecessarily
* Keep logic inside loop minimal and efficient

```

---

If you want, I can next:
- Turn this into a **reusable Java utility class (plug-and-play for interviews)**  
- Or give you **5 real HackerRank API problems with increasing difficulty**
```
