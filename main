import streamlit as st
import requests
import pandas as pd
import plotly.express as px

# Set up Streamlit app
st.title("🏀 NBA Live Stats & Predictions")
st.write("Get real-time NBA standings and predict game outcomes!")

# Fetch NBA Standings from an API (balldontlie.io or another service)
@st.cache_data
def get_nba_standings():
    url = "https://www.balldontlie.io/api/v1/teams"
    response = requests.get(url)
    if response.status_code == 200:
        teams_data = response.json()["data"]
        teams = pd.DataFrame(teams_data)[["full_name", "abbreviation", "conference", "division"]]
        return teams
    else:
        return pd.DataFrame()

teams_df = get_nba_standings()
if not teams_df.empty:
    st.write("### NBA Teams & Conferences")
    st.dataframe(teams_df)
else:
    st.write("Failed to fetch NBA data.")

# Simulating a simple game prediction (win probability based on random stats)
def predict_game(team1, team2):
    import random
    team1_score = random.randint(80, 120)
    team2_score = random.randint(80, 120)
    winner = team1 if team1_score > team2_score else team2
    return winner, team1_score, team2_score

# User selects two teams for prediction
st.write("### Predict a Game Outcome")
teams_list = teams_df["full_name"].tolist()
team1 = st.selectbox("Select Team 1", teams_list)
team2 = st.selectbox("Select Team 2", teams_list)

if st.button("Predict Winner 🏆"):
    winner, score1, score2 = predict_game(team1, team2)
    st.write(f"🏀 **{team1}**: {score1} vs **{team2}**: {score2}")
    st.write(f"🎉 Predicted Winner: **{winner}**")

# Display a sample visualization
st.write("### Team Win Probability Chart")
prob_data = pd.DataFrame({
    "Team": [team1, team2],
    "Win Probability": [random.randint(40, 60), random.randint(40, 60)]
})
fig = px.bar(prob_data, x="Team", y="Win Probability", title="Win Probability Comparison", color="Team")
st.plotly_chart(fig)
