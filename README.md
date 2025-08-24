# Sample bus routes (bus_id: list of stops)
bus_routes = {
    1: ["StopA", "StopB", "StopC", "StopD", "StopE"],
    2: ["StopF", "StopB", "StopG", "StopH", "StopE"],
    3: ["StopA", "StopI", "StopJ", "StopE"]
}

# Sample data for travel time (minutes), fare, and crowd level
bus_info = {
    1: {"time": 40, "fare": 20, "crowd": 30},  # 30 passengers
    2: {"time": 35, "fare": 15, "crowd": 50},  # 50 passengers
    3: {"time": 50, "fare": 10, "crowd": 20}   # 20 passengers
}


def recommend_route(start, end, preference="fastest"):
    recommendations = []
    for bus_id, route in bus_routes.items():
        if start in route and end in route:
            info = bus_info[bus_id]
            recommendations.append({
                "bus_id": bus_id,
                "route": route,
                "time": info["time"],
                "fare": info["fare"],
                "crowd": info["crowd"]
            })

    if not recommendations:
        return "❌ No direct bus route found."

    # Sort based on preference
    if preference == "fastest":
        recommendations.sort(key=lambda x: x["time"])
    elif preference == "cheapest":
        recommendations.sort(key=lambda x: x["fare"])
    elif preference == "least_crowded":
        recommendations.sort(key=lambda x: x["crowd"])

    return recommendations[0]  # best option


# -------- DEMO --------
start_point = "StopA"
end_point = "StopE"

print("Preference: Fastest")
print(recommend_route(start_point, end_point, "fastest"))

print("\nPreference: Cheapest")
print(recommend_route(start_point, end_point, "cheapest"))

print("\nPreference: Least Crowded")
print(recommend_route(start_point, end_point, "least_crowded"))
