

```
#include <iostream>
using namespace std;
int x_cord[11];
int y_cord[11];
int visited[11];
int home_x;
int home_y;
int min_dist = 999999;

int sum(int x,int y,int xx,int yy){
	int x_dist;
	int y_dist;
	if(x > xx) x_dist = x - xx;
	else x_dist = xx - x;
	if(y > yy) y_dist = y - yy;
	else y_dist = yy - y;
	return (x_dist + y_dist);
}

void find_all(int count,int x,int y,int n,int dist){
	if(dist > min_dist)
		return;

	if(count == n){
        dist += sum(x,y,home_x,home_y);
        if( dist < min_dist) min_dist = dist;
        return;
    }
    
    for(int i = 0; i < n; i++){
        if(visited[i] == 0){
            visited[i] = 1;
            dist += sum(x,y,x_cord[i],y_cord[i]);
            find_all(count+1,x_cord[i],y_cord[i],n,dist);
			dist -= sum(x,y,x_cord[i],y_cord[i]);
            visited[i] = 0;
        }
    }
}

int main()
{
   int T;
   cin >> T;
   int n;
   int office_x,office_y;
   
   for(int test_case = 1; test_case <= T; test_case++){
       min_dist = 99999;
       cin >> n >> office_x >> office_y >> home_x >> home_y;
       for(int i = 0; i < n; i++){
           cin >> x_cord[i] >> y_cord[i];
       }
       
       find_all(0,office_x,office_y,n,0);
	   cout << min_dist << endl;
   }     
   return 0;
}
```
