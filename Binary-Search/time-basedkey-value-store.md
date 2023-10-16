    class TimeMap {
        // map key => "given key"
        // map value => "the values associated with the key as an array of pair"
        // pair => {time, value}
        unordered_map<string, vector<pair<int, string>>> timeMap;
    public:
        TimeMap() {
            
        }
        
        void set(string key, string value, int timestamp) {
            // if there is no value associated with the key then initialize
            if(timeMap.find(key)==timeMap.end()){
                timeMap[key] = {make_pair(timestamp, value)};
            }
            else {
                // else push the value with timestamp
                timeMap[key].push_back({make_pair(timestamp, value)});
            }
        }
        
        string get(string key, int timestamp) {
            // get the list associated with the key
            vector<pair<int, string>> &list = timeMap[key];
            
            if(list.size() == 0){
                return "";
            }
    
            int low = 0, hi = list.size()-1, mid = (low+hi+1)/2;
            int ans = -1;
    
            // binary search on the list as because the list is already sorted
            // given input will have increasing timestamp for each key.
            // so the list will be automatically sorted
            while(low < hi){
    
                if(list[mid].first > timestamp){
                    hi = mid - 1;
                }
                else{
                    low = mid;
                    ans = mid;
                }
                mid = (low+hi+1)/2;
            }
    
            return list[mid].first <= timestamp ? list[mid].second : "";
        }
    };
    
    /**
     * Your TimeMap object will be instantiated and called as such:
     * TimeMap* obj = new TimeMap();
     * obj->set(key,value,timestamp);
     * string param_2 = obj->get(key,timestamp);
     */
