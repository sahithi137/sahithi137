class popularity_recommender():  
    def __init__(s):  
        s.t_data = None                                  
        s.u_id's = None                             
#ID'S of users  
        s.i_id's = None                               
#ID'S of Song users are listening to  
        s.pop_recommendations = None                
#getting all recommendations according to the popularity          
 #Creating the system models  
    def create_p(s, t_data, u_id's, i_id's):  
        s.t_data = t_data  
        s.u_id's = u_id's  
        s.i_id's = i_id's  
# Get a recommendation score based on the number of times each music has been listened to.  
        t_data_grouped = t_data.groupby([s.i_id's]).agg({s.u_id's: 'count'}).reset_index()  
        t_data_grouped.rename(columns = {'user_id's': 'score'},inpnlace=True)  
      
 #Sort the songs as per user ratings.  
        t_data_sort = t_data_grouped.sort_values(['score', s.i_id's], ascending = [0,1])  
      
#Create a ranking for recommendations based on score  
        t_data_sort['Rank'] = t_data_sort['score'].rank(ascending=0, method='first')  
          
        # top 10 recommendations are here  
        s.pop_recommendations = t_data_sort.head(10)  
 #To give recommendations using the system model   
def fits(dfs, algo, flag=0):  
    if flag:  
        algo.fits(df)  
    else:  
         algo.partial_fit(df)            
    dfs['label'] = algo.labels_  
    return (dfs, algo)  
In [ ]:  
def predict(t, Y):  
    y_preds = t[1].predict(Y)  
    modes = pd.Series(y_preds).mode()  
    return t[0][t[0]['label'] == mode.loc[0]]  
In [ ]:  
def recommend(recommendations, meta, Y):  
    dats = []  
    for i in Y['track_id']:  
        dats.append(i)  
    genre_modes = meta.loc[dat]['genres'].mode()  
    artist_modes = meta.loc[dat]['artist_name'].mode()  
    return metas[meta['genre'] == genre_mode.iloc[0]], meta[meta['artist_name'] == artist_modes.iloc[0]], meta.loc[recommendations['track_id']]  
In [ ]:  
t = fit(X, kmeans, 1)  
In [ ]:  
recommendations = predict(t, Y)  
In [ ]:  
output = recommend(recommendations, m)  
    def recommend_p(s, u_id's):      
        u1_recommendations = s.pop_recommendations  
          
        # Add the column for the user id where the music recommendations are generated.  
        u1_recommendations['user_id's'] = u_id's  
      
        #Bringing user_id's column to the upper front  
        cols = u1_recommendations.columns.tolist()  
        cols = cols[-1:] + cols[:-1]  
        u1_recommendations = u1_recommendations[cols]  
          
        return u1_recommendations  
