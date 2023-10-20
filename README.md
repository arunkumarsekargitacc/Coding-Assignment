package com.java;

import java.util.HashMap;
import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.List;
import java.util.Map;

public class RecentlyPlayedStore {
	private final int capacity;
	private Map<String, LinkedList<String>> recentlyPlayed;

	public RecentlyPlayedStore(int capacity) {
		this.capacity = capacity;
		this.recentlyPlayed = new LinkedHashMap<>();
	}
	public void addSong(String user, String song) {
		if (recentlyPlayed.containsKey(user)) {
			LinkedList<String> songs = recentlyPlayed.get(user);
			songs.remove(song);
			songs.addFirst(song);
			if (songs.size() > capacity) {
				songs.removeLast();
			}
		} else {
			LinkedList<String> songs = new LinkedList<>();
			songs.addFirst(song);
			recentlyPlayed.put(user, songs);
		}
	}

	public List<String> getRecentlyPlayedSongs(String user) {
		return recentlyPlayed.getOrDefault(user, new LinkedList<>());
	}
}
