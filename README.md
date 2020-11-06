
package football;

import junitparams.JUnitParamsRunner;
import junitparams.Parameters;
import org.junit.Test;
import org.junit.runner.RunWith;

import static junitparams.JUnitParamsRunner.$;
import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertTrue;

@RunWith(JUnitParamsRunner.class)
public class FootballTeamTest {
    private static final int TREE_GAMES_WON = 3;

    @Test
    public void constructorShouldSetGamesWon() {
        FootballTeam team = new FootballTeam(5);
        assertEquals("3 games passed to constructor, but "
                        + team.getGamesWon() + " were returned",
                5, team.getGamesWon());

    }

    public Object[] getNumbersOfWonGames() {
        return $(0, 1, 4);
    }

    @Test
    @Parameters(method = "getNumbersOfWonGames")
    public void constShouldSetGamesWon(int gamesWon) {
        FootballTeam footballTeam = new FootballTeam(gamesWon);
        assertEquals(gamesWon, footballTeam.getGamesWon());
    }

    @Test
    public void shouldBePossibleToCompareTeams() {
        FootballTeam team = new FootballTeam(TREE_GAMES_WON);
        assertTrue("FootballTeam should implement Comparable",
                team instanceof Comparable);
    }

    @Test
    public void teamsWithMoreMatchesShouldBeGreater() {
        FootballTeam team2 = new FootballTeam(2);
        FootballTeam team3 = new FootballTeam(3);
        assertTrue("Team with " + team3.getGamesWon() + " should be greater than team with " + team2.getGamesWon() + " games won", team3.compareTo(team2) > 0);
    }

    @Test
    public void teamsWithLessMatchesWonShouldBeLesser() {
        FootballTeam team2 = new FootballTeam(2);
        FootballTeam team3 = new FootballTeam(3);
        assertTrue("team with " + team2.getGamesWon()
                        + " games won should be ranked after the team with "
                        + team3.getGamesWon() + " games won",
                team2.compareTo(team3) < 0);
    }

    @Test
    public void teamsWithSameNumberOfMatchesWonShouldBeEqual() {
        FootballTeam teamA = new FootballTeam(2);
        FootballTeam teamB = new FootballTeam(2);
        assertTrue("both teams have won the same number of games: "
                        + teamA.getGamesWon() + " vs. " + teamB.getGamesWon()
                        + " and should be ranked equal",
                teamA.compareTo(teamB) == 0);
    }

}
